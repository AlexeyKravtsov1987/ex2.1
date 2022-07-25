ex 2.1

1. What is a Vertex shader responsible for and what is a fragment shader 
responsible for?

Vertex shader calculates new vertex positions by assigning them inside 
main() to gl_Position variable. Sometimes we can use it for 
assigning gl_PointSize if we work with points instead of lines or 
triangles, if we want to display some particles e.g. fire
Fragment shader calculates colors by assigning gl_FragColor inside its 
main. 

2. Which one of them is executed first? 

Vertex shader is executed first

3. What is an ‘attribute’ and what is a ‘uniform’? 

Both are types of pointers used to supplement GPU with data from CPU 
domain. Attribute is exclusive for Vertex shaders and contains vertex 
data. Attributes may be only a float, vec or mat. Attributes are designed 
to be dynamic (though it is disabled by default and should be enabled by 
glEnableVertexAttribArray()), only 8(16?) of them are permitted per 
program. Their location can be binded before shader linking with 
glBindAttribLocation

Uniforms are designed to be constant, may contain arrays and 128 of them 
are permitted inside a VSH, 16 inside a FSH. Their location can be only 
retrieved from a linked shader.

4. On which thread the ‘onDraw’ is called? 

SurfaceView in a contrast to a "normal" View would have its own thread 
governing how often it is redrawn. E.g., surfaceview attached to a 
CameraCaptureRequest would try to redraw on a new frame arrival. 
GLSurfaceView has an inner GLThread which 

either tries to continuously aquire lock in continuos mode to draw 
the latest rendered image 

or is limited by RENDERMODE_WHEN_DIRTY and waits for explicit 
requestRender() 

5. You wrote some code in the ‘MyRenderer’ which activated a shader, but 
how did it end up getting the view? What is the relation between 
‘MyGLSurfaceView’to ‘MyRenderer’. (Hint, ‘GLSurfaceView’ does a lot of 
work for you)

GLSurfaceView creates an EGLContext followed by 
- EGLDisplay so that the renderer (which was set via setRenderer 
method of a GLSurfaceView) can have where to place an output FrameBuffer
- EGLSurfaceWindow which will be visible to user through a "hole" in the 
activity View created by the SurfaceView
