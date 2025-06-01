
### ethmode command
| command |   status   |  
|---|---|
| ethmode l | only Port0,LAN |
| ethmode w | only Port0,WAN |
| ethmode wllll | Port0-Port4, Port0 is WAN,Port1-4 is LAN |
| ethmode lllll | Port0-Port4,all is LAN |


### wifimode command
| command |   status   |  
|---|---|
| wifimode ap | only AP,LAN |
| wifimode sta | only STA(apcli0),WAN |
| wifimode apsta | AP+STA,AP is LAN,STA is WAN |

### how to check if connected to some AP? use ap_client command,check return is ok or no
``` sh
$ ap_client
```
ok is connected
no is not connected

### How to compile?
# 1.install depend library
## Ubuntu 16.04
$ sudo apt-get update

$ sudo apt-get install git g++ make libncurses5-dev subversion libssl-dev gawk libxml-parser-perl unzip wget python xz-utils vim zlibc zlib1g zlib1g-dev openjdk-8-jdk build-essential ccache gettext xsltproc 
## Macos
note: install brew and Xcode command line tools

$brew install coreutils findutils gawk gnu-getopt gnu-tar grep wget quilt xz

note: gnu-getopt is keg-only, so force linking it:brew ln gnu-getopt --force

# 2.download the source use git
$ git https://kkgithub.com/imdenny/wireless-music.git
# 3.update the feeds
$ cd openwrt-hiwooya
$ ./scripts/feeds update -a

$ ./scripts/feeds install -a
# 4.config
$ make menuconfig
select the target:

Target System(Ralink RT288x/RT3xxx) --->

Subtarget(MT7688 based board) --->

Target Profile(HIWOOYA16128) --->

## note
HIWOOYA16128:16MB FLASH + 128MB RAM

HIWOOYA32128:32MB FLASH + 128MB RAM

HIWOOYA1664:16MB FLASH + 64MB RAM

HIWOOYA3264:32MB FLASH + 64MB RAM

# 5.make
$ make -j4 V=s

# 6.image
the binary image name like this in bin/ramips/:
openwrt-ramips-mt7688-Hiwooyaxxxxx-squashfs-sysupgrade.bin

# 7.change luci theme (TBD)
$ cd feeds/luci/themes
$ git clone -b 18.06 https://github.com/jerrykuku/luci-theme-argon.git
$ ./scripts/feeds update luci
$ ./scripts/feeds install luci-theme-argon
$ make menuconfig
$ --->LuCI -> Themes -> luci-theme-argon
$ make -j1 V=s

