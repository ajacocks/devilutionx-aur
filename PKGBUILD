# Maintainer: Alexander Jacocks <alexander@redhat.com>
pkgname=devilutionx
_pkgname=devilutionX
pkgver=1.2.1
pkgrel=1
pkgdesc="Diablo build for modern operating systems"
arch=('x86_64')
url="https://github.com/diasurgical/devilutionX"
#_url_d="https://github.com/diasurgical/devilutionX/archive/refs/tags"
#https://github.com/diasurgical/devilutionX/archive/refs/tags/1.2.1.zip
license=('Unlicense')
depends=('cmake' 'glibc' 'sdl2' 'sdl2_mixer' 'sdl2_ttf' 'libsodium' 'gcc-libs')
#source=(${pkgver}.zip::"${_url_d}/$pkgver.zip")
source=("git+https://github.com/diasurgical/$_pkgname#tag=${pkgver}"
        "${pkgname}.man")
sha256sums=('SKIP'
            '6db130612704b18c7b4ec770c5d36b1ef913b9dc3154c1402e691f3c73167df9')
build() {
  echo ln -sf ${srcdir}/${_pkgname} ${srcdir}/${pkgname}
  ln -sf ${srcdir}/${_pkgname} ${srcdir}/${pkgname}
  echo cd ${srcdir}/${pkgname}/build
  cd ${srcdir}/${pkgname}/build
  echo cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr
  cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr
  { test "$(nproc)" -gt 1 && echo make -j"$(nproc)" ;} || echo make
  { test "$(nproc)" -gt 1 && make -j"$(nproc)" ;} || make
}
package() {
  # install docs
  install -dm755 "$pkgdir"/usr/share/doc/$pkgname
  install -m0644 ${srcdir}/${pkgname}/docs/BACKGROUND.md "$pkgdir"/usr/share/doc/$pkgname/BACKGROUND.md
  install -m0644 ${srcdir}/${pkgname}/docs/building.md "$pkgdir"/usr/share/doc/$pkgname/building.md
  install -m0644 ${srcdir}/${pkgname}/docs/CHANGELOG.md "$pkgdir"/usr/share/doc/$pkgname/CHANGELOG.md
  install -m0644 ${srcdir}/${pkgname}/docs/CONTRIBUTING.md "$pkgdir"/usr/share/doc/$pkgname/CONTRIBUTING.md
  install -m0644 ${srcdir}/${pkgname}/docs/debug.md "$pkgdir"/usr/share/doc/$pkgname/debug.md
  install -m0644 ${srcdir}/${pkgname}/docs/installing.md "$pkgdir"/usr/share/doc/$pkgname/installing.md
  install -m0644 ${srcdir}/${pkgname}/docs/TODO.md "$pkgdir"/usr/share/doc/$pkgname/TODO.md
  install -m0644 ${srcdir}/${pkgname}/README.md "$pkgdir"/usr/share/doc/$pkgname/README.md
  install -m0644 ${srcdir}/${pkgname}/Packaging/nix/README.txt "$pkgdir"/usr/share/doc/$pkgname/README.txt
  # install package executable
  install -dm755 "$pkgdir"/usr/bin
  install -Dm755 ${srcdir}/${pkgname}/build/$pkgname "$pkgdir"/usr/bin/$pkgname
  # install package desktop files
  install -dm755 "$pkgdir"/usr/share/applications
  install -Dm644 ${srcdir}/${pkgname}/build/$pkgname.desktop "$pkgdir"/usr/share/applications/$pkgname.desktop
  install -Dm644 ${srcdir}/${pkgname}/build/$pkgname-hellfire.desktop "$pkgdir"/usr/share/applications/$pkgname-hellfire.desktop
  # install datafiles
  install -dm755 "$pkgdir"/usr/share/dissurgical/$pkgname
  install -Dm644 ${srcdir}/${pkgname}/Packaging/resources/$pkgname.mpq "$pkgdir"/usr/share/diasurgical/$pkgname/$pkgname.mpq
  # install icons
  install -dm755 "$pkgdir"/usr/share/icons/hicolor/512x512/apps
  install -Dm644 ${srcdir}/${pkgname}/Packaging/resources/icon.png "$pkgdir"/usr/share/icons/hicolor/512x512/apps/$pkgname.png
  install -Dm644 ${srcdir}/${pkgname}/Packaging/resources/hellfire.png "$pkgdir"/usr/share/icons/hicolor/512x512/apps/$pkgname-hellfire.png
  # install fonts
  install -dm755 "$pkgdir"/usr/share/fonts/TTF
  install -Dm644 ${pkgname}/Packaging/resources/CharisSILB.ttf "$pkgdir"/usr/share/fonts/TTF/CharisSILB.ttf
  # install license
  install -dm755 "$pkgdir"/usr/share/licenses/$pkgname
  install -m0644 ${pkgname}/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  # install man page
  install -Dm755 ${pkgname}.man "$pkgdir"/usr/share/man/man1/${pkgname}.1
  ln -sf "$pkgdir"/usr/share/man/man1/${pkgname}.1 "$pkgdir"/usr/share/man/man1/${pkgname}-hellfire.1
}
