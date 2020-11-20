# GnuTLS port of ngtcp2/examples

## Compiling

1. Build and install nghttp3, gnutls (patched), ngtcp2 in a dedicated directory ('$installdir' hereafter):
```sh
$ git clone https://github.com/ngtcp2/nghttp3.git
$ cd nghttp3
$ autoreconf -i
$ ./configure --prefix=$installdir --enable-lib-only
$ make -j$(nproc) check
$ make install
$ cd ..

$ git clone https://gitlab.com/gnutls/gnutls.git
$ cd gnutls
$ ./bootstrap
$ ./configure --prefix=$installdir --disable-doc --disable-guile
$ make -j$(nproc) check
$ make install
$ cd ..

$ git clone https://github.com/ngtcp2/ngtcp2.git
$ cd ngtcp2
$ autoreconf -i
$ ./configure --prefix=$installdir --enable-lib-only
$ make -j$(nproc) check
$ make install
$ cd ..
```

2. Compile with meson:
```sh
$ PKG_CONFIG_PATH=$installdir/lib/pkgconfig meson _build
$ ninja -C _build
```

## License

Follows the same license with ngtcp2, that is The MIT License.
