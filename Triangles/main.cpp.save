/* I'm learning opengl and playing around a bit. Following several tutorials and suplimenting
with a youtuber's tutorials (The Cherno)

Great resources:
	docs.gl - full descriptions of gl functions and their basic use.


. */


#include <iostream>
#include <string>
#include <math.h>

#include <GL/glew.h>
#include <GLFW/glfw3.h>

static GLuint compileShader(GLuint type, const std::string & src)
{
	GLuint id = glCreateShader(type);
	const char *source = src.c_str();
	glShaderSource(id, 1, &source, NULL);
	glCompileShader(id);

	int result;
	glGetShaderiv(id, GL_COMPILE_STATUS, &result);
	if(result == GL_FALSE)
	{
		int length;
		glGetShaderiv(id, GL_INFO_LOG_LENGTH, &length);
		char* msg = (char *) alloca(length * sizeof(char));
		glGetShaderInfoLog(id, length, &length, msg);
		std::cout << "Failed to compile "<< (type == GL_VERTEX_SHADER? "Vertex":"Fragment") << " shader:\n "  << msg << std::endl;
		glDeleteShader(id);
		return 0;
	}

	return id;
}

static GLuint createShader(const std::string & vertexShader, const std::string & fragmentShader)
{
	GLuint program  = glCreateProgram();
	GLuint vs = compileShader(GL_VERTEX_SHADER, vertexShader);
	GLuint fs = compileShader(GL_FRAGMENT_SHADER, fragmentShader);

	glAttachShader(program, vs);
	glAttachShader(program, fs);
	glLinkProgram(program);

	GLint success;
	GLchar infoLog[512];

	glGetProgramiv(program, GL_LINK_STATUS, &success);
	if(success == GL_FALSE)
	{
		glGetProgramInfoLog(program, 512, NULL, infoLog);
		std::cout << "ERROR Compilation failed: \n" << infoLog << std::endl;
	}

	glValidateProgram(program);

	glDeleteShader(vs);
	glDeleteShader(fs);

	return program;
}

void handle_keys(GLFWwindow * window, int key, int scancode, int action, int mode)
{
	if(key == GLFW_KEY_ESCAPE && action == GLFW_PRESS)
	{
		glfwSetWindowShouldClose(window, GL_TRUE);

	}
}



int main()
{
    GLFWwindow * wind = NULL;
    if(!(glfwInit())){
		std::cout << "Failed to call glfw\n";
		return -1;
    }
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
    glfwWindowHint(GLFW_RESIZABLE, GL_TRUE);

    wind = glfwCreateWindow(800, 600, "MY FIRST GLPROJECT: GLFW", NULL, NULL);
    glfwSetKeyCallback(wind,handle_keys);

    if(wind == NULL)
    {
    	std::cout << "Failed to create Window\n";
    	return -1;
    }
    glfwMakeContextCurrent(wind); //MUST be called before glewInit()
    glewExperimental = GL_TRUE;

    if(glewInit() != GLEW_OK)
    {
    	std::cout << "Glew Failed to initialize, must be done before calling GL functions\n";
    	return -1;
    }
    glClearColor(0.3, 0.3, 0.3, 0.5);
    glViewport(0,0,800, 600);
    GLfloat verts [] = {
    	-0.2, -0.5, 0.0,
    	0.5, -0.3, 0.0,
    	0.0, 0.5, 0.0
    };
    GLuint VAO;
	glGenVertexArrays(1, &VAO);
	glBindVertexArray(VAO);

    GLuint VBO;
    glGenBuffers(1, &VBO);
    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(verts), verts, GL_DYNAMIC_DRAW);



    int icount = 0;
    std::string vertShad = "#version 330 core \n"
    "	\n"
    "layout(location = 0) in vec4 position;\n"
    "	\n"
    "void main()\n"
    "{	\n"
    "	\n"
    "	\n"
    "	gl_Position = vec4(position.x, position.y, position.z, 1.0);\n"
    "}	\n"
    "\n";
    std::string fragShad = "#version 330 core \n"
    "	\n"
    "	\n"
    "out vec4 color;\n"
    "	\n"
    "	\n"
    "void main()\n"
    "{	\n"
    "	\n"
    "	\n"
    "	color = vec4(1.0f, 0.0f, 0.0f, 1.0f);\n"
    "}	\n";


    glVertexAttribPointer(0,3, GL_FLOAT, GL_FALSE, 3*sizeof(GLfloat), (GLvoid*)0);
	glEnableVertexAttribArray(0);
    GLuint shader = createShader(vertShad, fragShad);
	glUseProgram(shader);



    while (!(glfwWindowShouldClose(wind)))
    {
	    glClear(GL_COLOR_BUFFER_BIT);

	    glDrawArrays(GL_TRIANGLES, 0, 3);

    	glfwSwapBuffers(wind);
    	glfwPollEvents();

    }
	glDeleteProgram(shader);

    glfwTerminate();
	return 0;
}

