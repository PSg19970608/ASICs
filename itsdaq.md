# install itsdaq of v1 chips in centos7

mkdir sctdaq 
cd sctdaq 
mkdir sctvar 
cd sctvar 
mkdir ps data etc results config 
cd ..
git clone https://gitlab.cern.ch/atlas-itk-strips-daq/itsdaq-sw.git (the method of adding key:https://jaminzhang.github.io/git/config-and-add-SSH-key-in-GitLab/) (upload your own key to gitlab:https://gitlab.cern.ch/-/profile/keys)

cd itsdaq-sw/ 
python waf configure 
python waf build 
python waf install

ifconfig

mkfifo /tmp/hsioPipe.fromHsio mkfifo /tmp/hsioPipe.toHsio

sudo $SCTDAQ_ROOT/bin/hsioPipe --debug --eth enp0s8,e0:dd:cc:bb:aa:00 --file /tmp/hsioPipe.toHsio,/tmp/hsioPipe.fromHsio > /dev/null

(install digilent.adept.utilities-2.2.1.x86_64.rpm and digilent.adept.runtime-2.19.2.x86_64.rpm) 
djtgcfg enum 
djtgcfg init -d NexysVideo 
djtgcfg prog -d NexysVideo -i 0 --file 
djtgcfg prog -d NexysVideo -i 0 --file ./nexyfw/nexysv_itsdaq_vb48a_FSC_STAR_AV1EMU.bit

cd /home/sctdaq/sctdaq/itsdaq-sw 
export ROOTSYS=/usr 
export SCTDAQ_ROOT=/home/atlasitk/sctdaq/itsdaq-sw
export SCTDAQ_VAR=/home/atlasitk/sctdaq/sctvar
export SCTDB_USER=pk

./RUNITSDAQ.sh

some error as flows: error1:Please set SCTDAQ_VAR to point to config area: 
solution:source setup.sh

error2:TTi::TTi (viOpen) for UNKNOWN at resource /dev/serial/by-id/usb-TTi_MX_Series_PS U_483216-if00 failed with code 0xffffffff (TSerialProxy: IO Error) solution:change ./sctdaq/itsdaq-sw/macros/Stavelet.cpp,let variable Int_t lvtype = 0; Int_t hvtype =0;

error3:Read of status block failed! Failed to read from DAQ board to get initial status, closing connection 
solution:insert the network cable,set up wired network card (https://blog.csdn.net/yehuizhuang/article/details/79795603)

References: 
https://ipnp.cz/~kodys/works/daq_programs/Linux_ITKDAQ/QuickLinuxITKDAQInstall.html 
https://lighttomorrow.wordpress.com/2011/12/18/how-to-install-digilent-cable-driver-for-xilinx-design-suite-on-ubuntu-11-10/
