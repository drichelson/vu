vu
==

Vu (Virtual Universe) is a skeleton 3D engine written primarily in golang. 
Like many 3D engines vu is composed of various components which are detailed in the 
go docs and briefly summarized below.

Components
----------

* ``vu`` The 3D application facing layer wraps and extends the other components.
* ``vu/audio`` Audio provides an interface for positioning and playing sounds in a 3D environment. 
* ``vu/audio/al`` OpenAL bindings links the audio layer and the sound hardware. 
* ``vu/data`` Loaders for 3D resource data including models, textures, audio, shaders, and bitmapped fonts.
* ``vu/device`` Native support links the application to a OS specific window and user events. 
* ``vu/math/lin`` A vector, matrix, and quaternion math library.
* ``vu/physics`` Automatically reposition objects based on forces and collisions.
* ``vu/render`` Provides 3D drawing interface - abstracted from any particular technology.
* ``vu/render/gl`` Generated OpenGL golang bindings linking the rendering system and the graphics hardware.
* ``vu/render/gl/gen`` OpenGL binding generator. 

Less essential, but potentially more fun components are:

* ``vu/eg`` Examples that are used both to demonstrate (and verify) 3D engine functionality.
* ``vu/grid`` Grid based random level generators.

Build
-----

Build using ``./build src`` or ``python build src``.
All build output is located in the ``target`` directory.
Build and run the examples as in the ``vu\eg`` directory using ``go build`` and ``./eg``. 

**Build Dependencies**

Dependencies are kept to a minimum where possible. In general everything is text based
(better for source control) and can be developed in a command line environment (not saying 
IDE's are bad, just that there are no IDE dependencies or project files).

* go, GOPATH, and standard go libraries.  No external go packages are used.
* python for the source and documentation build scripts.
* ``osx``: Objective C and C compilers (clang) from XCode command line tools.
  Needs ``DYLD_LIBRARY_PATH`` set to find the ``vu/device/libvudev.1.dylib``.
  e.g. ``export DYLD_LIBRARY_PATH=$HOME/projects/vu/devices/libvudev.1.dylib``.
  This dependency may go away with golang 1.2.
* ``win``: C compiler (gcc) from mingw64-bit 
* pandoc for building documentation.
* git for source control and product version numbering.

Ignore python and pandoc if you want build by hand using ``go install``.  Check the
build script for the order. 

**Runtime Dependencies**

* OpenGL version 3.2 or later.
* OpenAL 64-bit version 2.1.

Limitations
-----------

Most components are bare bone by design (it's a skeleton 3D engine :). In particular:

* There is no games engine editor.
* Physics is only able to handle collision between a few shapes.  It is very limited in
  collision resolution and really has no concept of resting contact.  It needs replacement
  or porting from a real physics engine.
* Only one data format is supported for each type of 3D resource data, e.g ``.obj`` for 3D models.
* The device layer interface provides only the absolute minimum from the underlying windowing system. 
  OSX and Windows 7 are currently supported.
* Rendering supports standard OpenGL 3.2 and later. OpenGL extensions are ignored. 
* OpenGL may not be supported on all Windows graphics drivers (eg. laptop Intel based graphics)  
* 64-bit OpenAL may be difficult to locate for Windows machines 
  (http://connect.creativelabs.com/openal/Downloads/oalinst.zip if/when their website is up).
* Windows building has only been done using golang with gcc from mingw64-bit. 
  Building with Cygwin may have special needs. 

Overall the engine can produce only the simplest of simple 3D applications. Anything more 
should be using one of the many excellent commercial or open source engines.
