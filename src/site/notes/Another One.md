---
{"dg-publish":true,"permalink":"/another-one/"}
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D ASCII Animation</title>
    <style>
        @keyframes rotate {
            0% { transform: rotateX(0deg) rotateY(0deg); }
            100% { transform: rotateX(360deg) rotateY(360deg); }
        }
        .cube {
            font-family: monospace;
            font-size: 20px;
            line-height: 20px;
            white-space: pre;
            transform-style: preserve-3d;
            animation: rotate 5s infinite linear;
        }
        .face {
            position: absolute;
            width: 200px;
            height: 200px;
            backface-visibility: hidden;
        }
        .face:nth-child(1) { transform: rotateY(0deg) translateZ(100px); }
        .face:nth-child(2) { transform: rotateY(90deg) translateZ(100px); }
        .face:nth-child(3) { transform: rotateY(180deg) translateZ(100px); }
        .face:nth-child(4) { transform: rotateY(270deg) translateZ(100px); }
        .face:nth-child(5) { transform: rotateX(90deg) translateZ(100px); }
        .face:nth-child(6) { transform: rotateX(-90deg) translateZ(100px); }
    </style>
</head>
<body>
    <div class="cube">
        <div class="face">++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++</div>
        <div class="face">**********************************************************************</div>
        <div class="face">######################################################################</div>
        <div class="face">######################################################################</div>
        <div class="face">**********************************************************************</div>
        <div class="face">++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++</div>
    </div>
</body>
</html>