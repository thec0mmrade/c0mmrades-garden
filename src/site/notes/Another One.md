---
{"dg-publish":true,"permalink":"/another-one/"}
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D ASCII Sphere Animation</title>
    <style>
        @keyframes rotate {
            0% { transform: rotateY(0deg); }
            100% { transform: rotateY(360deg); }
        }
        .sphere {
            font-family: monospace;
            font-size: 15px;
            line-height: 15px;
            white-space: pre;
            transform-style: preserve-3d;
            animation: rotate 5s infinite linear;
            perspective: 1000px;
        }
        .layer {
            position: absolute;
            backface-visibility: hidden;
        }
        .layer:nth-child(1) { transform: translateZ(50px); }
        .layer:nth-child(2) { transform: translateZ(40px); }
        .layer:nth-child(3) { transform: translateZ(30px); }
        .layer:nth-child(4) { transform: translateZ(20px); }
        .layer:nth-child(5) { transform: translateZ(10px); }
        .layer:nth-child(6) { transform: translateZ(0px); }
    </style>
</head>
<body>
    <div class="sphere">
        <div class="layer">..........</div>
        <div class="layer">......@@......</div>
        <div class="layer">...@@@@@@@...</div>
        <div class="layer">..@@@@@@@@@..</div>
        <div class="layer">.@@@@@@@@@@@.</div>
        <div class="layer">@@@@@@@@@@@@@</div>
    </div>
</body>
</html>