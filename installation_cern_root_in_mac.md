Compile C language library FFTW supporting static library for iOS platform
(https://blog.csdn.net/shifang07/article/details/102579313)

installation of cern root in mac:


cd /home/software/root-6.26.06
sudo ./configure
sudo mkdir obj
cd obj
sudo cmake ..
sudo make -j4
sudo make install
sudo vim ~/.bash_profile
export PATH="$PATH:/home/software/root-6.26.06/obj/bin/thisroot.sh"
source ~/.bash_profile


References:
https://www.smooth-sysu.cn/software/root.html
https://www.hep.ucl.ac.uk/pbt/wiki/Software/ROOT
https://www.smooth-sysu.cn/software/root.html





