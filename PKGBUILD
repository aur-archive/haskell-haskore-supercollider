# Maintainer: Bernardo Barros <bernardobarros@gmail.com>
_hkgname=haskore-supercollider
pkgname=haskell-haskore-supercollider
pkgver=0.1.2.2
pkgrel=1
pkgdesc="Haskore back-end for SuperCollider"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('GPL')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-array=0.3.0.2' 'haskell-bytestring=0.9.1.10' 'haskell-containers' 'haskell-data-accessor<0.3' 'haskell-event-list<0.2' 'haskell-haskore<0.3' 'haskell-haskore-realtime<0.2' 'haskell-hosc<0.9' 'haskell-hsc3<0.9' 'haskell-non-negative<0.2' 'haskell-opensoundcontrol-ht<0.2' 'haskell-process=1.0.1.5' 'haskell-random=1.0.0.3' 'haskell-supercollider-ht<0.2' 'haskell-transformers=0.2.2.0' 'haskell-unix=2.4.2.0' 'haskell-utility-ht<0.1')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
md5sums=('a344bc647271fc09505f658c0f670463')
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O ${PKGBUILD_HASKELL_ENABLE_PROFILING:+-p } --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
