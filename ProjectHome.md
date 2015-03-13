# Update from 2012.04.18 #
Project moved to sf.net: http://sourceforge.net/projects/mingwbuilds/

# Update from 2012.04.02 #
The project mingw-builds provides the builds of GCC compiler for Windows 32/64 bit.

Up to now, the project was providing builds with two types of implementation of the exceptions: 1)**dwarf**, 2)**sjlj**.

The builds that use dwarf, will be excluded from the future builds of the project mingw-builds. This is due to two reasons:
  * for windows OS, dwarf is a foreign way to implement the exceptions. It can not work correctly in windows because the implementation of С++ and C(SEH) exceptions in MSVC compiler uses SJLJ. Due to this fact, are introduced subtle bugs coming from the destruction of the stack and throwing/catching of exceptions between dll-modules. You can see the opinions of the developers of CRT for MinGW(mingw-w64) [here](https://sourceforge.net/apps/trac/mingw-w64/wiki/Exception%20Handling).
  * and the second reason, which follows from the first - the absence of implementation of the dwarf for windows-x86\_64.

Builds are available for two architectures: 1)**i686**, 2)**x86\_64**.

Each of these build is dual-target cross-compiler.
The compiler for **i686** host, by default, builds for the **i686** target.
The compiler for **x86\_64** host, by default, builds for **x86\_64** target.

In order to build for **x86\_64** using a compiler for **i686** host, when compiling and linking add the flag **-m64**.

In order to build for **i686** using a compiler for **x86\_64** host, when compiling and linking add the flag **-m32**.

Of course, all dependencies should be built accordingly.

Now, about dependencies of the target on dll-modules distributed with the compiler (libstdc, etc ...):

As a rule, when using MinGW, the path to mingw/bin is prescribed PATH. All the dll-modules needed for the host, are also located in mingw/bin.
That's why, there are no problems with execution of the resulted executables. But when using a cross-compiler, things are a bit more complicated: in cases when host != target, dll-modules appear unavailable for the target executable.

For the **i686** compiler, the dll-modules for **x86\_64** target are located in mingw/i686-w64-mingw32/lib64.

For the **x86\_64** compiler, the dll-modules for **i686** target are located in mingw/x86\_64-w64-mingw32/lib32.

# Update from 2011.07.13 #
**Snapshots and releases builds of the MinGW compiler that use CRT & WinAPI from the mingw-w64 project.**

Builds support the following technologies:
  * OpenMP
  * LTO
  * Graphite
  * std\_threads
  * std\_atomics

Which built to choose? - That's it!

If you need a stable build, look for the builds names present "release". For example: 4.6.1-release-20110828 means that the GCC version 4.6.1 build, stable, build date 20110828. If the name of the built present "FINAL", it means that this latest build of this version of the compiler, and, as a rule - the best. If the suffix is "dwarf" - so this compiler implements exception using DWARF2 technology. Otherwise SJLJ.

**Тестовые и стабильные сборки компилятора MinGW использующего в качестве CRT и WinAPI проект mingw-w64.**

Сборки поддерживают следующие технологии:
  * OpenMP
  * LTO
  * Graphite
  * std\_threads
  * std\_atomics

Какую сборку выбрать? - Все просто!

Если Вам нужна стабильная сборка, ищите сборки в именах которых присутствует "release". Например: 4.6.1-release-20110828 означает, что это сборка GCC версии 4.6.1, стабильная, дата сборки 20110828. Если в имени сборки присутствует "FINAL", это означает, что это последняя сборка этой версии компилятора, и, как правило - лучшая. Если суффикс равен "dwarf" - значит этот компилятор реализует исключения используя DWARF2 технологию. Иначе SJLJ.