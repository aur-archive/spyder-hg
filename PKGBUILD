# Maintainer: willemw <willemw12@gmail.com>

_pkgname2=spyder
_pkgname3=spyder3
pkgbase=$_pkgname2-hg
pkgname=($_pkgname2-hg $_pkgname3-hg)
pkgver=r4391.c40dc14d316c
pkgrel=1
arch=('any')
url="https://bitbucket.org/spyder-ide/spyderlib"
license=('MIT')
makedepends=('python2-sphinx' 'python2-setuptools' 
             'python-sphinx' 'python-setuptools'
             'mercurial')
install=$pkgname.install
source=($_pkgname2::hg+https://bitbucket.org/spyder-ide/spyderlib)
md5sums=('SKIP')

pkgver() {
  cd $_pkgname2
  printf "r%s.%s" "$(hg identify -n)" "$(hg identify -i)"
} 

prepare() {
  cp -a $_pkgname2 $_pkgname3

  cd $_pkgname2

  # Patch PYLINT_PATH = programs.find_program('pylint')
  sed -i "s/find_program('pylint'/find_program('pylint2'/" spyderplugins/widgets/pylintgui.py
  # Patch process = subprocess.Popen(['pylint', '--version'],
  sed -i "s/subprocess.Popen(\['pylint'/subprocess.Popen(\['pylint2'/" spyderplugins/widgets/pylintgui.py
  # Patch match = re.match('(pylint|pylint-script.py) ([0-9\.]*)', lines[0])
  sed -i "s/re.match('(pylint|pylint-script.py/re.match('(pylint2|pylint2-script.py/" spyderplugins/widgets/pylintgui.py

  # Patch Python/Python2
  sed -i 's|#![ ]*/usr/bin/env python[ \t\r]*$|#!/usr/bin/env python2|' spyderlib/userconfig.py spyderlib/utils/external/pickleshare.py
}

build() {
  cd "$srcdir/$_pkgname2"
  python2 setup.py build

  cd "$srcdir/$_pkgname3"
  python setup.py build
}

package_spyder-hg() {
  pkgdesc="Scientific PYthon Development EnviRonment providing MATLAB-like features (Python 2 version)"
  depends=('python2-pyqt4' 'python2-pyflakes' 'python2-pyzmq' 'python2-pygments'
           'desktop-file-utils' 'gtk-update-icon-cache')
  optdepends=('python2-pylint: powerful code analysis'
              'ipython2: enhanced Python interpreter'
              'python2-rope: editor code completion, calltips and go-to-definition'
              'python2-sphinx: rich text help on the object inspector'
              'python2-numpy: N-dimensional arrays'
              'python2-scipy: signal/image processing'
              'python2-psutil: memory/CPU usage in the status bar'
              'python2-h5py: HDF5 support'
              'python2-matplotlib: interactive 2D/3D data plotting'
              'pep8-python2: real-time code style analysis'
              'python2-sympy: symbolic mathematics for the IPython console')
  _pkgname='spyder'
  provides=($_pkgname)
  conflicts=($_pkgname)

  cd $_pkgname
  python2 setup.py install --prefix=/usr --root="$pkgdir" --optimize=1
  # Install a scalable icon for the spyder.desktop file
  install -Dm644 spyderlib/images/spyder.svg "$pkgdir/usr/share/icons/hicolor/scalable/apps/spyder.svg"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  rm "$pkgdir/usr/bin/spyder_win_post_install.py"
}

package_spyder3-hg() {
  pkgdesc="Scientific PYthon Development EnviRonment providing MATLAB-like features (Python 3 version)"
  depends=('python-pyqt4' 'python-pyflakes' 'python-pyzmq' 'python-pygments'
           'desktop-file-utils' 'gtk-update-icon-cache')
  optdepends=('python-pylint: powerful code analysis'
              'ipython: enhanced Python interpreter'
              'python-rope: editor code completion, calltips and go-to-definition'
              'python-sphinx: rich text help on the object inspector'
              'python-numpy: N-dimensional arrays'
              'python-scipy: signal/image processing'
              'python-psutil: memory/CPU usage in the status bar'
              'python-h5py: HDF5 support'
              'python-matplotlib: interactive 2D/3D data plotting'
              'pep8: real-time code style analysis'
              'python-sympy: symbolic mathematics for the IPython console')
  _pkgname='spyder3'
  provides=($_pkgname)
  conflicts=($_pkgname)

  cd $_pkgname
  python setup.py install --prefix=/usr --root="$pkgdir" --optimize=1
  # Install a scalable icon for the spyder3.desktop file
  install -Dm644 spyderlib/images/spyder.svg "$pkgdir/usr/share/icons/hicolor/scalable/apps/spyder3.svg"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  rm "$pkgdir/usr/bin/spyder_win_post_install.py"
}

