---
title: GPGPU Installations
author: aaditya prakash
layout: page
dsq_thread_id:
- 
---

!TODO add the header info

# Upgrade the Ubuntu
 These are the google doc links of the presentations I have given in class, or seminars or other invited talks. These were the most requested urls !

  * sudo apt-get update        # Fetches the list of available updates
  * sudo apt-get upgrade       # Strictly upgrades the current packages
  * sudo apt-get dist-upgrade  # Installs updates (new ones)

# Partition and mount the harddrives

  * sudo apt-get install -y mdadm   # Install mdadm
  * sudo mdadm --assemble --scan    # check for existing raids ## found existing !! If not prepeare, refer tutorial here http://askubuntu.com/questions/526747/setting-up-raid-1-on-14-04-with-an-existing-drive

## Mounting
  * df -aTh                         # shows list of all mounts
  ### Manual mount
  * sudo mount /dev/md0 /media/hdd/ # monnt existing 
  ### Mount permanently
  * blkid                           # shows uuid for drives to add to fstab
  Add the following line to /etc/fstab
    # the RAID 1 mount of two hdd
    UUID=06ad59d9-3176-4c16-95e9-77356cc572d7       /media/hdd      ext2    defaults    0    1
  * sudo mount -a                   # mount using fstab

# Install Essentials, extras Git / Zsh 
  * sudo apt-get install -y build-essential
  * sudo apt-get install -y ubuntu-restricted-extras
  * sudo apt-get install -y vim
  * sudo apt-get install -y git
  * sudo apt-get install -y git-core
  * sudo apt-get install -y zsh
  * sudo apt-get install -y tmux
  * sudo apt-get install -y CMake
  * sudo apt-get install -y libopenblas-dev
  * sudo apt-get install -y gcc-4.8 # because CUDA works will less than 4.9.0
    * make soft link for gcc in /usr/bin
  * sudo apt-get install -y g++-4.8 # because CUDA works will less than 4.9.0
    * make soft link for g++ in /usr/bin
  * sudo apt-get install -y apache2
    * sudo /etc/init.d/apache2 start # start the Apache Server


# Python and Libs
  * python get-pip.py # install pip
  * sudo apt-get install python-dev # pythonLibs 
  * sudo apt-get install libblas-dev liblapack-dev libatlas-base-dev gfortran
  * sudo pip install numpy
  * sudo pip install cython git+https://github.com/scipy/scipy # Installs Cython and Scipy both (Cython is requirement for scipy)
  * sudo pip install -U scikit-learn # Requires numpy and scipy
  * sudo pip install nose
  * sudo pip install markupsafe

  ## Python3 and Ipython (Jupyter)
  * sudo apt-get install python3-pip
  * sudo pip install jupyter
  * sudo pip3 install jupyter # I don't know why it requires sepearate installation, especially when not done using Anaconda !
   

# Customization
  * chsh -s `which zsh`             # Change the shell to ZSH
  * sudo reboot now                 # Requires restart
  * git clone git@github.com:iamaaditya/dotfiles.git
  * ~/dotfiles/install.sh           # Run the commands to make the shortcuts
  * git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim # Install bundle
  ## Solarized Color for vim
      * cd ~/.vim/colors/ 
      * wget https://raw.githubusercontent.com/altercation/vim-colors-solarized/master/colors/solarized.vim
  ## Powerline & associated fonts
  * pip install powerline-status    # Powerline 
    * wget https://github.com/Lokaltog/powerline/raw/develop/font/PowerlineSymbols.otf https://github.com/Lokaltog/powerline/raw/develop/font/10-powerline-symbols.conf
    * mkdir -p ~/.fonts/ && mv PowerlineSymbols.otf ~/.fonts/
    * fc-cache -vf ~/.fonts
    * mkdir -p ~/.config/fontconfig/conf.d/ && mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/
    Note - if some aspects of powerline does not show up, check <http://askubuntu.com/questions/283908/how-can-i-install-and-use-powerline-plugin>

# Install NVIDIA Drivers
  * # Download AMD 64 bit Linux drivers from NVIDIA website (manual download and transfer)
  * sudo service lightdm stop       # stop the X server before running the installation
    !! Could not sign kernels, make a note of this. It might lead to problems with some libraries later on

# Install CUDA
  * sudo ./cuda_7.0.28_linux.run --override  # for cuda 7.0
  * sudo ln -s /usr/bin/g++-4.8 /usr/local/cuda/bin/g++
  * sudo ln -s /usr/bin/gcc-4.8 /usr/local/cuda/bin/gcc

# Install GPU Libraries

## Theano
  * sudo pip install Theano
  * sudo apt-get install -y python-pycuda # also installs the dependencies, but it is best to have own installation of nvidia-cuda, to make sure the version is proper and to maintain multiple version installation

## Tensorflow
  * sudo pip install --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.6.0-cp27-none-linux_x86_64.whl
  Tensorflow (as of Jan 15, 2016), works on Cuda 7.0 and CuDNN v2 ), thus change /usr/local/cuda softlink

## Keras
  * sudo pip install keras

## Lasagne
  * sudo pip install https://github.com/Lasagne/Lasagne/archive/master.zip

# Optional
## Remove unnecessary Ubuntu folders
 * rm -rf ~/Desktop
 * rm -rf ~/Public # Is not persistent, after restart Ubuntu recreates this directory
 * rm -rf ~/Pictures
 * rm -rf ~/Music
 * rm -rf ~/Videos
 * rm -rf ~/Downloads
 * rm -rf ~/Templates
 * rm -rf ~/Documents
 * rm -rf ~/examples.desktop
