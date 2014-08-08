# Maintainer: Jean-Christophe Saad-Dupy <jc.saaddupuy@fsfe.org>
# Contributor: Jean-Christophe Saad-Dupy <jc.saaddupuy@fsfe.org>
pkgname=m116-SS7300-fixkeyboard
pkgver=0.1
pkgrel=1
pkgdesc="Keyboard fix for m116-SS7300 laptop"
arch=(any)
license=('WTFPL')
install='PKGBUILD'
 

prepare(){
    # pakage is self contains : create the src layout
  mkdir -p $srcdir/etc/systemd/system/
  mkdir -p $srcdir/usr/local/bin/
  
  cat >  $srcdir/etc/systemd/system/fix-laptop-issues.service <<EOF
[Unit]
Descrition=Fix laptop issues such as keyboard release keys

[Service]
ExecStart=/usr/local/bin/fix-laptop-issues.sh

[Install]
WantedBy=multi-user.target
EOF
  
 cat >  $srcdir/usr/local/bin/fix-laptop-issues.sh <<EOF
#!/bin/bash
echo 86,369-370 > /sys/bus/serio/devices/serio0/force_release
EOF


}

build() {
  # create the pkg layout
  mkdir -p $pkgdir/etc/systemd/system/
  mkdir -p $pkgdir/usr/local/bin/

  # copy files to the pkgdir
  cp $srcdir/etc/systemd/system/fix-laptop-issues.service $pkgdir/etc/systemd/system/
  cp $srcdir/usr/local/bin/fix-laptop-issues.sh $pkgdir/usr/local/bin/
}


post_install() {
    echo "Enabling systemd service"
    systemctl enable fix-laptop-issues.service
    echo "Starting systemd service"
    systemctl start fix-laptop-issues.service
}

post_upgrade() {
    echo "Reloading systemd"
    systemctl daemon-reload
}


