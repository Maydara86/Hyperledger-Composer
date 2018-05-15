# BlockChain Lab

[![N|Solid](https://blockchainacuity.com/images/logos/hyperledger_logo_256x256.png)](https://nodesource.com/products/nsolid)

# Things to do

  - Prevent Docker Instalation in script shell 
```sh
# Install docker
function install_docker ()
{
       if [[ $DOCKER_INSTALL == "true" ]]; then
	 	showStep "Ensure that CA certificates are installed"
		sudo apt-get -y install apt-transport-https ca-certificates

		showStep "Add Docker repository key to APT keychain"
		curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

		showStep "Update where APT will search for Docker Packages"
		echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu ${CODENAME} stable" | \
		    sudo tee /etc/apt/sources.list.d/docker.list

		showStep "Update package lists"
		sudo apt-get update

		showStep "Verifies APT is pulling from the correct Repository"
		sudo apt-cache policy docker-ce

		showStep "Install kernel packages which allows us to use aufs storage driver if V14 (trusty/utopic)"
		if [ "${CODENAME}" == "trusty" ]; then
		    showStep "Installing required kernel packages"
		    sudo apt-get -y install linux-image-extra-$(uname -r) linux-image-extra-virtual
		fi

		showStep "Install Docker"
		sudo apt-get -y install docker-ce

		showStep "Add user account to the docker group"
		sudo usermod -aG docker $(whoami)

        showStep "Installing docker-composer"
        sudo curl -L https://github.com/docker/compose/releases/download/1.16.0-rc1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose -o /usr/local/bin/docker-compose
        sudo chmod +x /usr/local/bin/docker-compose

	else
		showStep "${RED} docker installation skipped"
	fi
}
```
