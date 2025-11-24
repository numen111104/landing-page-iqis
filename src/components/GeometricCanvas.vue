<script setup>
import { onMounted, onBeforeUnmount, ref } from 'vue';

const canvasRef = ref(null);
let ctx = null;
let animationFrameId;
let mouse = { x: 0, y: 0 };
let time = 0;

// Konfigurasi Mandala
const config = {
    segmentCount: 8, // Segi 8 (Rub el Hizb style)
    layers: 6, // Jumlah lapisan kedalaman
    baseSpeed: 0.002,
    color: '#fcdd33' // Kuning IQIS
};

function drawMandala(centerX, centerY) {
    // Efek Parallax halus berdasarkan mouse
    const offsetX = (mouse.x - centerX) * 0.05;
    const offsetY = (mouse.y - centerY) * 0.05;

    for (let l = 1; l <= config.layers; l++) {
        const radius = l * 60 + (Math.sin(time * 2 + l) * 10); // Efek "Bernafas"
        const rotation = time * (l % 2 === 0 ? 1 : -1) * config.baseSpeed * l + (l * 0.2);
        const alpha = 0.15 - (l * 0.02); // Semakin luar semakin transparan

        ctx.strokeStyle = `rgba(252, 221, 51, ${alpha})`;
        ctx.lineWidth = 1.5;

        ctx.save();
        ctx.translate(centerX - offsetX * (l / 2), centerY - offsetY * (l / 2));
        ctx.rotate(rotation);

        ctx.beginPath();
        for (let i = 0; i < config.segmentCount; i++) {
            const angle = (Math.PI * 2 / config.segmentCount) * i;
            const nextAngle = (Math.PI * 2 / config.segmentCount) * (i + 1);

            // Titik sudut luar
            const x1 = Math.cos(angle) * radius;
            const y1 = Math.sin(angle) * radius;

            // Titik sudut dalam (membuat bentuk bintang)
            const innerRadius = radius * 0.7; // Rasio bintang
            const midAngle = angle + (Math.PI / config.segmentCount);
            const xMid = Math.cos(midAngle) * innerRadius;
            const yMid = Math.sin(midAngle) * innerRadius;

            // Gambar garis geometri
            if (i === 0) ctx.moveTo(x1, y1);
            else ctx.lineTo(x1, y1);

            ctx.lineTo(xMid, yMid);
        }
        ctx.closePath();
        ctx.stroke();

        // Tambahkan ornamen titik di sudut
        ctx.fillStyle = `rgba(252, 221, 51, ${alpha * 2})`;
        for (let i = 0; i < config.segmentCount * 2; i++) {
            const angle = (Math.PI / config.segmentCount) * i;
            const r = i % 2 === 0 ? radius : radius * 0.7;
            const x = Math.cos(angle) * r;
            const y = Math.sin(angle) * r;

            ctx.beginPath();
            ctx.arc(x, y, 2, 0, Math.PI * 2);
            ctx.fill();
        }

        ctx.restore();
    }
}

function animate() {
    ctx.clearRect(0, 0, canvasRef.value.width, canvasRef.value.height);

    // Background gradient halus agar tidak flat
    const gradient = ctx.createRadialGradient(
        canvasRef.value.width / 2, canvasRef.value.height / 2, 0,
        canvasRef.value.width / 2, canvasRef.value.height / 2, canvasRef.value.width
    );
    gradient.addColorStop(0, 'rgba(2, 100, 50, 0)');
    gradient.addColorStop(1, 'rgba(0, 30, 15, 0.4)'); // Vignette hijau gelap
    ctx.fillStyle = gradient;
    ctx.fillRect(0, 0, canvasRef.value.width, canvasRef.value.height);

    time += 0.01;

    // Gambar Mandala di tengah
    drawMandala(canvasRef.value.width / 2, canvasRef.value.height / 2);

    animationFrameId = requestAnimationFrame(animate);
}

const handleResize = () => {
    canvasRef.value.width = innerWidth;
    canvasRef.value.height = innerHeight;
};

const handleMouseMove = (e) => {
    mouse.x = e.clientX;
    mouse.y = e.clientY;
};

onMounted(() => {
    ctx = canvasRef.value.getContext('2d');
    handleResize();
    mouse.x = innerWidth / 2;
    mouse.y = innerHeight / 2;

    window.addEventListener('resize', handleResize);
    window.addEventListener('mousemove', handleMouseMove);

    animate();
});

onBeforeUnmount(() => {
    window.removeEventListener('resize', handleResize);
    window.removeEventListener('mousemove', handleMouseMove);
    cancelAnimationFrame(animationFrameId);
});
</script>

<template>
    <canvas ref="canvasRef"
        class="absolute top-0 left-0 w-full h-full pointer-events-none z-0 mix-blend-screen"></canvas>
</template>