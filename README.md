# buildroot
This is the build environment for the engine. The majority of the logic is contained here [izackp/engine](https://github.com/izackp/engine).

I wanted to simplify the overall build environment, so I switched the project from using gsync for dependencies to github submodules. (Which is still in progress atm)

For whoever is reading this, I still have a few more things to do. I've gotten the project successfully build after removing dart from the project. Its not at the point where you can just grab this and use this as a library. I may or may not need to make modifications and/or simplifications. The project was originally designed to run as the base/main loop of the program. It becomes the platform for a Dart VM that is tied to most of the APIs. However, My goal is to turn it into a usable library which means drastically changing that aspect.

Getting this project into a usable state is pretty much the first milestone.
Some of the things I'm working on:
* Make it easier for people to pick up the code and work on it
* * Instructions, Simplier tools, examplanation of the build process and gn, explanations on what does what in the code
* Create a sample project that utilizes the flutter engine for rendering (windows)

#### Building the Project

#### TODO
* Some git commits needed are unreachable since we're using shallow checkout for submodules. 
* GitKraken Glo looks dope. See how well integration works
* Add Instructional documention for checking out the code.
* Add instructions on how to build the project and use GN (GN is the build system for this project; it replaces CMAKE)
* Create Outline Documentation on the overall heirachy of the code. (What is lib/ui, shell, runtime, ect)

#### Milestones
* Working C++ Desktop Example for Windows
* Then Linux, and OSX
* Then Android and iOS
* Modify the API for ease of use and portablility (Ex: What do we need to do to integrate this into a Unity game? How will events be handled between the main app and this library? Will/Can this library handle rendering or do I need to pass a sort of command list to the hosting application to render?)
* Create a 'standard library' of UI elements (tables, constraints, ect)
* Create a UI Builder