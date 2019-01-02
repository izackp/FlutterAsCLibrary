# buildroot
Originally the build environment for the Flutter engine, but now its a modified build environment for a modified version of Flutter. 

The majority of the logic is contained here [izackp/engine](https://github.com/izackp/engine).

I want to simplify the overall build environment, so I switched the project from using gsync for dependencies to github submodules. 

For whoever is reading this, I still have a few more things to do. I've gotten the project successfully build after removing dart from the project. Its not at the point where you can just grab this and use this as a library. I may or may not need to make modifications and/or simplifications. The project was originally designed to run as the base of the program. It becomes the platform for a Dart VM that is tied to most of the APIs. However, My goal is to turn it into a usable library which means drastically changing that aspect.

Getting this project into a usable state is pretty much the first milestone. 
Some of the things I'm working on:
* Make it easier for people to pick up the code and work on it
* * Instructions, Simplier tools, examplanation of the build process and gn, explanations on what does what in the code
* Create a sample project that utilizes the flutter engine for rendering (windows)