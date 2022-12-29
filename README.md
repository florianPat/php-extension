# PHP Extension

A PHP-Extension just for fun, maybe something evolves here? Who knows...

### Building

To debug this extension (on linux) install the build tools, gdb, valgrind and what other stuff you need:

`package-manager install build-essential autoconf automake bison flex re2c gdb libtool make pkgconf valgrind git`

Then clone the interpreter source and switch branches:
- `git clone https://github.com/php/php-src.git`
- `cd php-src`
- `git checkout PHP-8.2`

Then build php:
- `mkdir php-build`
- `./buildconf --force`
- `./configure --enable-debug --prefix=/your-php-src-dir/php-build/DEBUG --with-config-file-path=/your-php-src-dir/php-build/DEBUG/etc` (for more options see ./configure --help, for example nts/zts build or directly include extensions in binary)
- `export CORE_COUNT=`nproc``
- `make -j$CORE_COUNT`
- `make install`
- `cd ..`
- `mkdir /your-php-src-dir/php-build/DEBUG/etc` and put the php.ini file into it
- Add the new php executable to your path (/your-php-src-dir/php-build/DEBUG/bin)
- Check that stuff works by running `php -v`
- Now create an extension skeleton with: `php ./ext/ext_skel.php --ext name-of-extension --dir path-where-the-ext-should-get-created`
- Follow the output steps to build the extension into a shared library
- Add `extension=name-of-extension.so` as a new line in the php.ini file
- With `php -m` the new extension should show up and you should be able to call the registered function by running `php -r test_test1();`
- Get started on developing extensions. Some links with cool information:
  - https://www.zend.com/sites/default/files/pdfs/whitepaper-zend-php-extensions.pdf
  - https://kchodorow.com/2011/08/11/php-extensions-made-eldrich-installing-php/
  - https://youtu.be/WMOI2U8McTE
  - https://www.phpinternalsbook.com/
  - https://externals.io/
  - https://www.npopov.com/
  - https://www.zend.com/blog/debugging-php-segmentation-faults

### Debugging

Attach with gdb and use the gdbinit script from php-src. Steps follow...
