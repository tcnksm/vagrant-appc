Vagrant.configure('2') do |config|
  config.vm.box = "ubuntu/trusty64" # Ubuntu 14.04
  config.vm.provision :shell,inline: <<EOF
ROCKET_VERSION=v0.1.1
echo "Install rocket ${ROCKET_VERSION}"
mkdir rocket
wget https://github.com/coreos/rocket/releases/download/${ROCKET_VERSION}/rocket-${ROCKET_VERSION}.tar.gz
tar xzvf rocket-${ROCKET_VERSION}.tar.gz -C rocket --strip-components=1
rm rocket-${ROCKET_VERSION}.tar.gz
sudo mv rocket/rkt /usr/local/bin/.

APP_SPEC_VERSION=v0.1.1
echo "Install actool ${APP_SPEC_VERSION}"
wget https://github.com/appc/spec/releases/download/${APP_SPEC_VERSION}/appc-spec-${APP_SPEC_VERSION}.tar.gz
mkdir app-spec
tar xzvf appc-spec-${APP_SPEC_VERSION}.tar.gz -C app-spec --strip-components=1
rm appc-spec-${APP_SPEC_VERSION}.tar.gz
echo 'export PATH=/home/vagrant/app-spec:$PATH' >> /home/vagrant/.bashrc

EOF
end
