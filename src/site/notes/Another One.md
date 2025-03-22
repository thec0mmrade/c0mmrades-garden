---
{"dg-publish":true,"permalink":"/another-one/"}
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D ASCII Pyramid Animation</title>
    <style>
        body {
            background-color: black;
            color: white;
            font-family: monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }
        #pyramid {
            white-space: pre;
            font-size: 24px;
            line-height: 1.1;
            transform-style: preserve-3d;
            animation: rotate 5s infinite linear;
        }
        @keyframes rotate {
            from {
                transform: rotateY(0deg);
            }
            to {
                transform: rotateY(360deg);
            }
        }
    </style>
</head>
<body>
    <div id="pyramid">
        <!-- ASCII Art of Pyramid -->
        <pre>
             /\  
            /  \  
           /    \  
          /      \  
         /        \  
        /__________\  
         \        /  
          \      /  
           \    /  
            \  /  
             \/  
        </pre>
    </div>
</body>
</html>
