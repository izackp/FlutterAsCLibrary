# buildroot
This is the build environment for the modified flutter engine. The majority of the logic is contained here [izackp/engine](https://github.com/izackp/engine).

I wanted to simplify the overall build environment, so I switched the project from using gsync for dependencies to github submodules. Subtrees are pretty tempting, but I need to do some more research first. I like the idea that a copy of the code will be in the repo and that it will be easier to checkout, but I don't like the idea of polluting the git history and the alleged difficulty of pushing up changes. Again, I need to do more research.

For whoever is reading this, I still have a few more things to do. I've gotten the project to successfully build after removing dart from the project. It's not at the point where you can just grab this and use this as a library. I may or may not need to make modifications and/or simplifications. The project was originally designed to run as the base/main loop of the program. It becomes the platform for a Dart VM which is then tied to most of the APIs. However, my goal is to turn it into a usable library which means drastically changing that aspect.

Getting this project into a usable state is pretty much the first milestone.
Some of the things I'm working on:
* Make it easier for people to pick up the code and work on it
* * Instructions, Simplier tools, explanation of the build process and gn, explanations on what does what in the code
* Create a sample project that utilizes the flutter engine for rendering (windows)

#### Checking out the code
* Clone the repo
* ```git clone git@github.com:izackp/FlutterAsCLibrary.git``` (add: ```--depth 1``` for shallow)

Full Submodules:
* ```git submodule update --init --recursive```

Shallow Submodules (Faster; takes less space):
I recommend to do this, but only if you're comfortable with git
* ```git submodule update --init --depth 1 --recursive```
* skia and libwebp won't work. You will need to cd into the directories fetch their respective branches noted in .gitmodules (flutter/1.0 and 0.6.0), cd back out then re run the command. (If anyone knows how to fix this, feel free to contact me!)
* You may need to increase the depth or do a full checkout if the commit we're using gets behind
* Be aware that using the depth argument may put the submodules in a state where it's tracking only master. If this is the case then no matter what you do (git pull or fetch) you will only get the master branch from remote.origin.
``` 
git config --get remote.origin.fetch
+refs/heads/master:refs/remotes/origin/master
```

If you need a branch other than master then you need to change the above in .git/config to this:
```
+refs/heads/*:refs/remotes/origin/*
```

#### Building the Project
* Follow the above to checkout out the code.
* Get chrome's [depot_tools](http://commondatastorage.googleapis.com/chrome-infra-docs/flat/depot_tools/docs/html/depot_tools_tutorial.html#_setting_up) and add it to the path (Windows: ```$env:Path += ";C:\Dev_Tools\depot_tools"```)
* cd into the repo and run ```gn gen out```. This will generate ninja files into the `out` folder.
* cd into `out` and run `ninja`.
* If you're using windows refer to the notes at the bottom of this readme

#### TODO
* ~~Some git commits needed are unreachable when using -depth 1 option checkout for submodules. I would like to make the repo easy to checkout, so I may fork some of the dependecies so they may be accessable without downloading 2GB of data.~~
* ~~Add Instructional documention for checking out the code.~~
* ~~Add instructions on how to build the project~~ and use GN (GN is the build system for this project; it replaces CMAKE)
* Create Outline Documentation on the overall heirachy of the code. (What is lib/ui, shell, runtime, ect)

#### Milestones
* ~~Remove DART~~ _done_
* Working C++ Desktop Example for Windows
* Modify the API for ease of use and portablility (Ex: What do we need to do to integrate this into a Unity or Mono game? How will events be handled between the main app and this library? Will/Can this library handle rendering or do I need to pass a sort of command list to the hosting application to render?)
* Then Linux, and OSX
* Then Android and iOS
* Create C Interface
* Create a 'standard library' of UI elements (tables, constraints, ect; Will be seperate project)
* Maybe build C# / DLang wrappers to the C Interface.
* Create a UI Builder

#### Dependencies Overview
If I know where, why, how something is used. I'll mention it here otherwise I don't immediately know.
* benchmark - Tools for measuring performance. Lost of tests and related stuff has been taken out. I kept this because it seems like it could be useful.
* icu - [What is ICU?](http://site.icu-project.org/#TOC-What-is-ICU-) Handles a lot of text stuff. Used in paragraph builder (txt mentioned below).
* expat - (Embedded; not a submodule) XML Parser.
* freetype2 - Font Library.
* googletest - Unit testing library.
* gyp - Google's previous build system. Scripts in here _seem_ to be needed for the build process.
* harfbuzz - A text shaping library. Not sure where it's used.
* libjpeg-turbo - Decodes jpegs.
* libpng - Decodes pngs.
* libwebp - Decodes webp.
* libxml - Seems to be another xml library. _TODO: What is the difference between this and expat?_
* rapidjson - Decodes json.
* skia - A complete 2D graphic library for drawing Text, Geometries, and Images.
* vulkan - Vulkan headers and Docs. API for the graphics card.
* zlib - Data compression library.
* flutter - The main source code.
* flutter/third_party/txt - (Embedded; not a submodule) Seems to handle everything that has to do with text that can be represented with data. Styling, integration with Skia, ect.

#### Misc Notes
* [Windows] To get the windows cl.exe compiler to work. (Might be fixed in the newest version). The folder containing the repo needs case sensitivity disabled. Otherwise, you'll get ```c1xx: fatal error C1083: Cannot open source file``` errors.
* [Windows/VSCode] To get cpp plugins in vscode to work. The root folder(?) needs case sensitivity disabled.
```
Disable: fsutil.exe file setCaseSensitiveInfo path disable
Enable : fsutil.exe file setCaseSensitiveInfo path enable
Query  : fsutil.exe file queryCaseSensitiveInfo path
```