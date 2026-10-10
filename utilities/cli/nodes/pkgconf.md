# pkgconf

- Get the list of libraries and their dependencies:

`pkgconf --libs {{library1 library2 ...}}`

- Get the list of libraries, their dependencies, and proper cflags for gcc:

`pkgconf --cflags --libs {{library1 library2 ...}}`

- Print the version of the linked modules:

`pkgconf --modversion {{module1 module2 ...}}`

- Compile your code with libgtk-3, libwebkit2gtk-4.0, and all their dependencies:

`c++ example.cpp $(pkgconf --cflags --libs gtk+-3.0 webkit2gtk-4.0) -o example`
