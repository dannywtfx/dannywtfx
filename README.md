<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Efecto Tecnológico para Daniel García</title>
<style>
/* Estilos básicos para el cuerpo y contenedor */
body, html {
    height: 100%;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #0d1117; /* Fondo oscuro tipo GitHub */
    font-family: 'Roboto Mono', monospace; /* Fuente monoespaciada para aspecto tecnológico */
    overflow: hidden; /* Evitar barras de desplazamiento si la animación sobresale */
}

/* Contenedor principal de la animación */
.tech-glitch-container {
    position: relative;
    padding: 20px;
    background: #0d1117;
}

/* El texto principal de "DANIEL GARCÍA" */
.glitch-text {
    font-size: 6rem; /* Tamaño muy grande */
    font-weight: 800;
    text-transform: uppercase;
    color: #fff; /* Texto blanco principal */
    letter-spacing: -2px;
    position: relative;
    z-index: 10;
}

/* Pseudo-elementos ::before y ::after para crear las capas de glitch y color */
.glitch-text::before,
.glitch-text::after {
    content: "DANIEL GARCÍA"; /* El texto duplicado */
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    opacity: 0.8;
}

/* Capa ::before: Color cian (capa "roja" del glitch) */
.glitch-text::before {
    color: #0ff; /* Cian/Azul tecnológico */
    z-index: -1;
    animation: glitch-anim-1 2.5s infinite linear alternate-reverse;
}

/* Capa ::after: Color magenta (capa "azul" del glitch) */
.glitch-text::after {
    color: #f0f; /* Magenta */
    z-index: -2;
    animation: glitch-anim-2 2s infinite linear alternate-reverse;
}

/* EFECTO DE LÍNEA HORIZONTAL ESCANEANDO DETRÁS */
.scanner-line {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background-color: #2da44e; /* Verde tecnológico */
    opacity: 0.7;
    border-radius: 2px;
    z-index: 5;
    transform: translateY(-100%);
    animation: scan-move 4s linear infinite;
    filter: blur(1px);
}

/* KEYFRAMES PARA LA PRIMERA CAPA DE GLITCH (Cian) */
@keyframes glitch-anim-1 {
    0% {
        clip: rect(30px, 9999px, 10px, 0);
        transform: translate(-3px, -2px);
    }
    10% {
        clip: rect(2px, 9999px, 45px, 0);
        transform: translate(2px, 2px);
    }
    20% {
        clip: rect(98px, 9999px, 81px, 0);
        transform: translate(-1px, 1px);
    }
    30% {
        clip: rect(65px, 9999px, 91px, 0);
        transform: translate(3px, -3px);
    }
    40% {
        clip: rect(81px, 9999px, 49px, 0);
        transform: translate(0px, 0px);
    }
    50% {
        clip: rect(2px, 9999px, 66px, 0);
        transform: translate(-1px, -1px);
    }
    60% {
        clip: rect(110px, 9999px, 30px, 0);
        transform: translate(2px, 3px);
    }
    70% {
        clip: rect(9px, 9999px, 75px, 0);
        transform: translate(-2px, -2px);
    }
    80% {
        clip: rect(44px, 9999px, 98px, 0);
        transform: translate(1px, -3px);
    }
    90% {
        clip: rect(101px, 9999px, 4px, 0);
        transform: translate(3px, 1px);
    }
    100% {
        clip: rect(12px, 9999px, 50px, 0);
        transform: translate(0px, 0px);
    }
}

/* KEYFRAMES PARA LA SEGUNDA CAPA DE GLITCH (Magenta) */
@keyframes glitch-anim-2 {
    0% {
        clip: rect(76px, 9999px, 11px, 0);
        transform: translate(2px, -1px);
    }
    10% {
        clip: rect(40px, 9999px, 63px, 0);
        transform: translate(-1px, 3px);
    }
    20% {
        clip: rect(109px, 9999px, 20px, 0);
        transform: translate(3px, -2px);
    }
    30% {
        clip: rect(12px, 9999px, 110px, 0);
        transform: translate(-2px, 2px);
    }
    40% {
        clip: rect(61px, 9999px, 98px, 0);
        transform: translate(0px, -3px);
    }
    50% {
        clip: rect(90px, 9999px, 1px, 0);
        transform: translate(1px, -1px);
    }
    60% {
        clip: rect(10px, 9999px, 76px, 0);
        transform: translate(-3px, 3px);
    }
    70% {
        clip: rect(3px, 9999px, 80px, 0);
        transform: translate(2px, 0px);
    }
    80% {
        clip: rect(88px, 9999px, 100px, 0);
        transform: translate(-1px, -2px);
    }
    90% {
        clip: rect(44px, 9999px, 2px, 0);
        transform: translate(3px, 2px);
    }
    100% {
        clip: rect(70px, 9999px, 55px, 0);
        transform: translate(0px, 0px);
    }
}

/* KEYFRAMES PARA EL MOVIMIENTO DE LA LÍNEA DE ESCANEO */
@keyframes scan-move {
    0% {
        transform: translateY(-100%);
        opacity: 0;
    }
    10% {
        transform: translateY(0%);
        opacity: 0.7;
    }
    90% {
        transform: translateY(100vh); /* Mover fuera de la vista hacia abajo */
        opacity: 0.7;
    }
    100% {
        transform: translateY(100vh);
        opacity: 0;
    }
}
</style>
</head>
<body>

<div class="tech-glitch-container">
    <div class="glitch-text">Daniel García</div>
    <div class="scanner-line"></div>
</div>

</body>
</htm
