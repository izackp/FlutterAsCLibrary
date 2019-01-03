# buildroot
This is the build environment for the engine. The majority of the logic is contained here [izackp/engine](https://github.com/izackp/engine).

I wanted to simplify the overall build environment, so I switched the project from using gsync for dependencies to github submodules. (Which is still in progress atm). Though I am a little concerned about using shallow checkout. If the dependency doesn't follow the remote HEAD commit closely then it won't be able to properly checkout the module. This still allows use to have a local repo way smaller than the 2GB it would normally take. Also, people more than likely already know how to use git submodules over gsync.

For whoever is reading this, I still have a few more things to do. I've gotten the project successfully build after removing dart from the project. Its not at the point where you can just grab this and use this as a library. I may or may not need to make modifications and/or simplifications. The project was originally designed to run as the base/main loop of the program. It becomes the platform for a Dart VM that is tied to most of the APIs. However, my goal is to turn it into a usable library which means drastically changing that aspect.

Getting this project into a usable state is pretty much the first milestone.
Some of the things I'm working on:
* Make it easier for people to pick up the code and work on it
* * Instructions, Simplier tools, examplanation of the build process and gn, explanations on what does what in the code
* Create a sample project that utilizes the flutter engine for rendering (windows)

#### Building the Project

#### TODO
* Some git commits needed are unreachable since we're using shallow checkout for submodules. 
* Add Instructional documention for checking out the code.
* Add instructions on how to build the project and use GN (GN is the build system for this project; it replaces CMAKE)
* Create Outline Documentation on the overall heirachy of the code. (What is lib/ui, shell, runtime, ect)

#### Milestones
* -Remove DART- _done_
* Working C++ Desktop Example for Windows
* Then Linux, and OSX
* Then Android and iOS
* Modify the API for ease of use and portablility (Ex: What do we need to do to integrate this into a Unity game? How will events be handled between the main app and this library? Will/Can this library handle rendering or do I need to pass a sort of command list to the hosting application to render?)
* Create C Interface
* Create a 'standard library' of UI elements (tables, constraints, ect; Will be seperate project)
* Maybe build C# / DLang wrappers to the C Interface.
* Create a UI Builder

#### Dependencies Overview
If I know where, why, how something is used. I'll mention it here otherwise I don't immediately know.
* benchmark - Tools for measuring performance. Lost of tests and related stuff has been taken out. I kept this because it seems like it could be useful.
* icu - [What is ICU?](http://site.icu-project.org/#TOC-What-is-ICU-). Handles a lot of text stuff. Used in paragraph builder (txt mentioned below).
* expat - XML Parser.
* freetype2 - Font Library.
* googletest - Unit testing library.
* gyp - Google's previous build system. Scripts in here _seem_ to be needed for the build process.
* harfbuzz - A text shaping library. Not sure where it's used.
* libjpeg-turbo - Decodes jpegs obviously.
* libpng - Decodes pngs.
* libwebp - Decodes webp.
* libxml - Seems to be another xml library. _TODO: What is the difference between this and expat?_
* rapidjson - Decodes json.
* skia - A complete 2D graphic library for drawing Text, Geometries, and Images.
* vulkan - Vulkan headers and Docs. API for the graphics card.
* zlib - Data compression library.
* flutter - The main source code.
* flutter/third_party/txt - (Embedded; not a submodule) Seems to handle everything that has to do it with text that can be represented with data. Styling, Integration with Skia, ect.