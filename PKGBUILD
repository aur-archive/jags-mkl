# Maintainer: jdarch <jda -dot- cloud -plus- archlinux -at- gmail -dot- com>
# Based on the 'jags' package in AUR made by:
# Contributor: miggy <jkomdl at gmail dot com>
# Contributor: Keith Schnakenberg <keith dot schnakenberg at gmail dot com>

pkgname=jags-mkl
_pkgname=jags
pkgver=3.4.0
pkgrel=2
pkgdesc="Bayesian hierarchical models using Markov Chain Monte Carlo (MCMC) simulation, linked with Intel MKL"
arch=('x86_64 i686')
url="http://mcmc-jags.sourceforge.net/"
license=('GPL')
depends=('intel-mkl' 'libtool' 'libltdl')
options=('!libtool')
provides=('jags=3.4.0')
conflicts=('jags')
install=jags-mkl.install
makedepends=('gcc-fortran' 'intel-mkl')

source=(http://downloads.sourceforge.net/project/mcmc-jags/JAGS/3.x/Source/JAGS-$pkgver.tar.gz)
md5sums=('ac8242931837e4367b2a3de8b231aa0e')
sha512sums=('7a330ea41eab63b23d8ae3622c6920f0dc3dba653a18256957b9b862bb86b746ff706e9e9bf3f806524250b439161a6df4ad05af682354073f9b0074f9825896')

if [ "$CARCH" == "x86_64" ]; then
    _intel_arch=intel64
    _intel_lib=mkl_gf_lp64
elif [ "$CARCH" == "i686" ]; then
    _intel_arch=ia32
    _intel_lib=mkl_gf
fi

build () {
        # Set up the environment for MKL
        source /opt/intel/mkl/bin/mklvars.sh ${_intel_arch}
        _mkllibs=" -fopenmp -Wl,--no-as-needed -L${MKLROOT}/lib/intel64 -l${_intel_lib} -lmkl_core -lmkl_gnu_thread -ldl -lpthread -lm"

	cd "$srcdir/JAGS-$pkgver"
	./configure --prefix=/usr --libexecdir=/usr/lib/${_pkgname} --with-blas="${_mkllibs}" --with-lapack="${_mkllibs}"
	make
}
package() {
	cd "$srcdir/JAGS-$pkgver"
	make DESTDIR="$pkgdir/" install
}
