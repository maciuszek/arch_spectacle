# Maintainer: Matt Kuzminski <mattkuzminski at gmail dot com>

_pkgname=spectacle
pkgname="nodejs-$_pkgname"
pkgver=git
pkgrel=1
pkgdesc="Spectacle generates beautiful static HTML5 documentation from OpenAPI/Swagger 2.0 API specifications"
arch=('any')
url="https://github.com/sourcey/$_pkgname"
license=('MIT')
depends=('nodejs')
makedepends=('npm' 'jq')
source=("$_pkgname"::"git+$url.git")
sha256sums=('SKIP')

build() {
  cd $srcdir/$_pkgname
  npm install
  npm pack
}

package() {
  cd $srcdir/$_pkgname
  npm install -g --user root --prefix "$pkgdir"/usr ./$_pkgname-docs-`jq -r .version package.json`.tgz

  # Non-deterministic race in npm gives 777 permissions to random directories.
  # See https://github.com/npm/npm/issues/9359 for details.
  find "${pkgdir}"/usr -type d -exec chmod 755 {} +

  # npm gives ownership of ALL FILES to build user
  # https://bugs.archlinux.org/task/63396
  chown -R root:root "$pkgdir"
}
