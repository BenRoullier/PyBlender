# Installing Blender as a Python Module on Windows (64 bit)
  
These instructions should allow you to install blender 2.80 as both a fully featured GUI based program and as a module (bpy) which can be imported into Python. **It&#39;s probably best to uninstall any existing copies of Blender and Python before you do this** , in order to avoid version conflicts.
  
1. Install the following programs (all free):
  1. [VisualStudio IDE 2017 Community Edition](https://visualstudio.microsoft.com/)
    1. When installing, select the &quot;Desktop development with C++&quot; workflow
  2. [Subversion for Windows (SlikSVN)](https://sliksvn.com/download/)
  3. [Git for Windows](https://gitforwindows.org/)
    1. Ensure you choose the &quot;add git to PATH&quot; option
  4. [CMake](https://cmake.org/download/)
    1. Ensure you add CMake to path for all users

2. Create a location to act as your blender repository. These instructions assume you choose C:\blender\_repo

3. Open a command prompt and navigate to your blender repository

4. Use the following command to download the precompiled blender binaries:
SVN checkout https://svn.blender.org/svnroot/bf-blender/trunk/lib/win64\_vc14 lib/win64\_vc14_

5. Use the following commands in order to download the latest blender source code:
_git clone git://git.blender.org/blender.git
cd blender
git submodule update --init --recursive
git submodule foreach git checkout master
git submodule foreach git pull --rebase origin master_

6. Use this command to build the full blender with a GUI:
_make full_

7. In Windows, navigate to C:\blender\_repo\build\_windows\_Full\_x64\_vc15\_Release\bin\Release 
This folder contains blender.exe, which is the launcher for the GUI (you might want to create a shortcut to here from your desktop and/or start menu)

8. Determine which version of python your blender install is using. You **MUST** install the same version of python yourself (see step 10):
  1. Launch blender.exe
  2. Press _CTRL + Page Up_ to open the scripting view
  3. The python console (left hand side) should contain a line something like:
&quot;PYTHON INTERACTIVE CONSOLE 3.7.0 (default, Aug 26 2018, 16:05:01) …&quot;
  4. In this case, the version is 3.7.0
  5. Close Blender

9. Go back to the command prompt and use the following command to build the blender python module:
_make bpy_

10. While the python module is building, [install python](https://www.python.org/downloads/).
  1. **Ensure you get the EXACT SAME version you identified in step 8.3**
  2. Ensure you check the &quot;add python to PATH&quot; box.
  3. You might want to do a custom install, in particular to put python into a more sensible location than the default. These instructions assume you install it to C:\Python37

11. Once the _make bpy_ process has completed, go back to the command prompt and run the following commands in order to copy the blender python module to your python install:
_cd ..
cd build\_windows\_Bpy\_x64\_vc15\_Release\bin
copy Release\bpy.pyd C:\Python37\Lib\site-packages\
copy Release\*.dll C:\Python37\Lib\site-packages\
xcopy /E/I Release\2.80 C:\Python37\2.80_

12. You should now be able to import blender as a python module in any script file with the line
_import bpy_
  
GOOD LUCK!