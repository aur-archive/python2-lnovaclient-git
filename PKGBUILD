# Maintainer: Troy C < rstrox -ta yahoo -tod com >

pkgname=python2-lnovaclient-git
pkgver=20140120
pkgrel=2
pkgdesc="Python bindings to the Rackspace Legacy Cloud Servers API"
arch=('any')
url="https://github.com/cloudnull/python-lnovaclient"
license=('GPL')
depends=('python2-distribute' 'python2-iso8601' 'python2-prettytable' 'python2-httplib2' 'python2-simplejson')
makedepends=('git')
provides=('python2-lnovaclient')
conflicts=('python2-lnovaclient')
_gitroot='https://github.com/cloudnull/python-lnovaclient.git'
_gitname='python-lnovaclient'

build() {
        cd "${srcdir}"
        msg "Connecting to GIT server...."

        if [[ -d "${_gitname}" ]]; then
        cd "${_gitname}" && git pull origin
        msg "The local files are updated."
        else
        git clone "${_gitroot}" "${_gitname}"
        fi

        msg "GIT checkout done or server timeout"
        msg "Starting make..."

        rm -rf "$srcdir/$_gitname-build"
        git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
        REV=$(git show-ref --abbrev --heads | cut -f 1 -d\ )
	cd "$srcdir/$_gitname-build"
	sed -i'' 's/prettytable==0.5/prettytable>=0.5/g' setup.py
        python2 setup.py build
}
package() {
        cd "$srcdir/$_gitname-build"
        python2 setup.py install --root=${pkgdir}
}

