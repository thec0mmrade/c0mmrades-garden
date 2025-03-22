---
{"dg-publish":true,"permalink":"/home/","tags":["gardenEntry"]}
---

Welcome to c0mmrade's digital garden thing.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Shader in HTML</title>
</head>
<body style="margin: 0; overflow: hidden;">
    <canvas id="glCanvas" width="800" height="600"></canvas>
    
    <script id="fragmentShader" type="x-shader/x-fragment">
        precision mediump float;
        uniform float u_time;
        uniform vec2 u_resolution;
        
        void main() {
            vec2 uv = gl_FragCoord.xy / u_resolution.xy;
            
            // Create a colorful gradient based on position and time
            vec3 color = vec3(
                0.5 + 0.5 * sin(uv.x * 6.0 + u_time),
                0.5 + 0.5 * sin(uv.y * 5.0 + u_time * 0.7),
                0.5 + 0.5 * sin((uv.x + uv.y) * 4.0 + u_time * 1.3)
            );
            
            gl_FragColor = vec4(color, 1.0);
        }
    </script>
    
    <script id="vertexShader" type="x-shader/x-vertex">
        attribute vec2 a_position;
        void main() {
            gl_Position = vec4(a_position, 0.0, 1.0);
        }
    </script>
    
    <script>
        // Initialize everything when the window loads
        window.onload = function() {
            const canvas = document.getElementById('glCanvas');
            const gl = canvas.getContext('webgl');
            
            if (!gl) {
                alert('WebGL not supported in your browser');
                return;
            }
            
            // Resize canvas to window size
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            gl.viewport(0, 0, canvas.width, canvas.height);
            
            // Create shader program
            const vertexShaderSource = document.getElementById('vertexShader').textContent;
            const fragmentShaderSource = document.getElementById('fragmentShader').textContent;
            const program = createProgram(gl, vertexShaderSource, fragmentShaderSource);
            
            // Look up uniform locations
            const timeUniformLocation = gl.getUniformLocation(program, 'u_time');
            const resolutionUniformLocation = gl.getUniformLocation(program, 'u_resolution');
            
            // Create a position buffer for a full-screen quad
            const positionBuffer = gl.createBuffer();
            gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
            
            // Two triangles forming a quad that covers the entire clip space
            const positions = [
                -1, -1,
                 1, -1,
                -1,  1,
                -1,  1,
                 1, -1,
                 1,  1
            ];
            gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(positions), gl.STATIC_DRAW);
            
            // Animation loop
            let startTime = Date.now();
            function render() {
                // Update time and resolution
                const currentTime = (Date.now() - startTime) * 0.001; // Convert to seconds
                gl.useProgram(program);
                gl.uniform1f(timeUniformLocation, currentTime);
                gl.uniform2f(resolutionUniformLocation, canvas.width, canvas.height);
                
                // Setup position attribute
                const positionAttributeLocation = gl.getAttribLocation(program, 'a_position');
                gl.enableVertexAttribArray(positionAttributeLocation);
                gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
                gl.vertexAttribPointer(positionAttributeLocation, 2, gl.FLOAT, false, 0, 0);
                
                // Draw the quad
                gl.drawArrays(gl.TRIANGLES, 0, 6);
                
                // Request next frame
                requestAnimationFrame(render);
            }
            render();
            
            // Handle window resize
            window.addEventListener('resize', function() {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
                gl.viewport(0, 0, canvas.width, canvas.height);
            });
        };
        
        // Helper function to create a shader
        function createShader(gl, type, source) {
            const shader = gl.createShader(type);
            gl.shaderSource(shader, source);
            gl.compileShader(shader);
            
            if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS)) {
                console.error('Shader compilation error:', gl.getShaderInfoLog(shader));
                gl.deleteShader(shader);
                return null;
            }
            
            return shader;
        }
        
        // Helper function to create a program
        function createProgram(gl, vertexSource, fragmentSource) {
            const vertexShader = createShader(gl, gl.VERTEX_SHADER, vertexSource);
            const fragmentShader = createShader(gl, gl.FRAGMENT_SHADER, fragmentSource);
            
            const program = gl.createProgram();
            gl.attachShader(program, vertexShader);
            gl.attachShader(program, fragmentShader);
            gl.linkProgram(program);
            
            if (!gl.getProgramParameter(program, gl.LINK_STATUS)) {
                console.error('Program linking error:', gl.getProgramInfoLog(program));
                return null;
            }
            
            return program;
        }
    </script>
</body>
</html>
```