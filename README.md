# domoticz2022_a20_0penwrt19.07.7   first install liblua5.3 , lua5.3 , minizip then domoticz into openwrt

to be able to compile for your own  device that not cortexA7 follow these steps
 download 19.07.x version you would like to use I used 19.07.07 but you can use others
 
 https://github.com/openwrt/openwrt/tags?after=v22.03.0-rc2
 
  extract  and cd into openwrt folder
  run ./scripts/feeds update -a
 
  now download and extract
  https://github.com/krywenko/domoticz2022_a20_0penwrt19.07.7/blob/main/domoticz-2022.tar.gz
.  
.  
now edit  tool/cmake/makerfile  to
PKG_VERSION:=3.16.1
PKG_HASH:=a275b3168fa8626eca4465da7bb159ff07c8c6cb0fb7179be59e12cbdfa725fd

or replace the makefile from the compress folder /tools/cmake

next copy cereal and minizip folder to packages/libs folder

and then copy lua5.3 folder to packages/util folder

you can edit packages.index with the information  found in text file called  modifications feeds/packages.index in your openwrt dir

now run ./scripts/feeds install -a

once that is done  you can copy replace the domoticz folder  in feed/packages/util with the one from the compressed folder

after that  you can run make menuconfig   addin your device format and enable domoticz

 then
 
 run make -j1 V=s
 
 you should olny get one  error when it compiling  EnOceanRawValue.cpp  you now need to edit this file  it fouund in the build_dir  it will be listed with the error where it is located
 
 now add this to it
 
 #include <cstring> 
 
 and modify the  error  from  ----> srtsrt to std::strsrt
 
  save  then rerun make -j1 V=s again
  and everything should compile fully now and make your installer packages 
  if not
 
  then run make -j1 V=s /package/domoticz/compile
 
   you will get the EnOceanRawValue.cpp again just edit it again   
 
 run make -j1 V=s /package/domoticz/compile


