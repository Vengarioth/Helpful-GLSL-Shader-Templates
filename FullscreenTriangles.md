#Fast & easy way to draw fullscreen effects

__Vertex Shader__
```glsl
#version 330

void main() {
    vec2 texCoord = vec2((gl_VertexID << 1) & 2, gl_VertexID & 2);
    gl_Position = vec4(texCoord * vec2(2.0f, -2.0f) + vec2(-1.0f, 1.0f), 0.0f, 1.0f);
}
```
__Fragment Shader__
```glsl
#version 330
precision highp float;

vec2 ViewportSize; //the size of the viewport, something like 1280, 720

void main(void) {
    vec2 fragmentCoordinate = gl_FragCoord.xy / ViewportSize;
    gl_FragColor = vec4(fragmentCoordinate.x, fragmentCoordinate.y, 0, 1);
}
```
Invoke the shader in c/c++
```c
glDrawArrays(GL_TRIANGLE_STRIP, 0, 4);
```
Or in C# with OpenTK
```csharp
GL.DrawArrays(PrimitiveType.TriangleStrip, 0, 4);
```

PS: Don't use fullscreen Quads, Triangles result in better usage of the rasterization process, google it if you need proof :)