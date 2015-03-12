Vagrant.configure('2') do |config|
  # Ubuntu 14.04
  config.vm.box = "ubuntu/trusty64"

  # Docker
  config.vm.provision :docker

  # Install appc tools & rocket
  config.vm.provision :shell,inline: <<EOF

echo 'Install dependencies...'
sudo apt-get update -y 
sudo apt-get install --no-install-recommends -y -q \
                     curl \
                     build-essential \
                     ca-certificates \
                     git mercurial bzr \

GOVERSION=1.4.2
echo "Install Go v${GOVERSION}"
mkdir /home/vagrant/goroot
mkdir -p /home/vagrant/gopath/bin
curl https://storage.googleapis.com/golang/go${GOVERSION}.linux-amd64.tar.gz \
           | tar xvzf - -C /home/vagrant/goroot --strip-components=1

export GOROOT=/home/vagrant/goroot
export GOPATH=/home/vagrant/gopath
export PATH=$GOROOT/bin:$GOPATH/bin:$PATH
# echo 'export GOROOT=/home/vagrant/goroot' >> /home/vagrant/.bashrc
# echo 'export GOPATH=/home/vagrant/gopath' >> /home/vagrant/.bashrc
# echo 'export PATH=$GOROOT/bin:$GOPATH/bin:$PATH' >> /home/vagrant/.bashrc

RKTVERSION="v0.4.0"
echo "Install Rocket ${RKTVERSION}"
cd /tmp
wget https://github.com/coreos/rocket/releases/download/${RKTVERSION}/rocket-${RKTVERSION}.tar.gz
tar xzvf rocket-${RKTVERSION}.tar.gz
cp rocket-${RKTVERSION}/* ${GOPATH}/bin/.

echo "Install actool"
go get -d github.com/appc/spec
cd ${GOPATH}/src/github.com/appc/spec
./build
cp bin/* ${GOPATH}/bin/.

echo "Install docker2aci"
go get github.com/appc/docker2aci

echo "Install goaci"
go get github.com/appc/goaci

sudo cp ${GOPATH}/bin/* /usr/local/bin/.
EOF

end
