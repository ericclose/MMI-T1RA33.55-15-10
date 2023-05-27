# MMI-T1RA33.55-15-10 For Motorola edge 20 pro

## Kernel Modules

```bash
top_dir=$PWD

mkdir -vp $top_dir/kernel_platform/build

cd $top_dir/kernel_platform/build/

git clone https://android.googlesource.com/kernel/build

mv build kernel

mkdir -vp $top_dir/kernel_platform/prebuilts/

cd $top_dir/kernel_platform/prebuilts/

git clone https://android.googlesource.com/kernel/prebuilts/build-tools/

mkdir -vp $top_dir/prebuilts/clang/host/

cd $top_dir/prebuilts/clang/host/

git clone https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86

mkdir -vp $top_dir/prebuilts/gcc/linux-x86/host

cd $top_dir/prebuilts/gcc/linux-x86/host

git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/host/x86_64-linux-glibc2.17-4.8

mkdir -vp $top_dir/prebuilts/gas/

cd $top_dir/prebuilts/gas/

git clone https://android.googlesource.com/platform/prebuilts/gas/linux-x86

cd $top_dir/kernel_platform

git clone https://android.googlesource.com/kernel/common
```

Download kernel source code. Rename `kernel-msm` folder to `$top_dir/kernel_platform/msm-kernel`

```bash
export my_top_dir=$PWD/kernel_platform

export ROOT_DIR="$my_top_dir"

PATH=$my_top_dir/out/msm-kernel-kalama-gki/host/bin:$my_top_dir/build/kernel/build-tools/path/linux-x86:$my_top_dir/prebuilts/clang/host/linux-x86/clang-r450784e/bin:$PATH

export AR="llvm-ar" ARCH="arm64" CC="clang" DEPMOD="depmod" DTC="$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc" HOSTCC="clang" LD="ld.lld" NM="llvm-nm" OBJCOPY="llvm-objcopy" OBJDUMP="llvm-objdump" OBJSIZE="llvm-size" TARGET_BUILD_VARIANT=user TARGET_PRODUCT="rtwo" STRIP="llvm-strip" LLVM="1" HOSTCXX="clang++" HOSTCFLAGS="--sysroot=$my_top_dir/build/kernel/build-tools/sysroot  -I$my_top_dir/prebuilts/kernel-build-tools/linux-x86/include " HOSTLDFLAGS="--sysroot=$my_top_dir/build/kernel/build-tools/sysroot  -Wl,-rpath,$my_top_dir/prebuilts/kernel-build-tools/linux-x86/lib64 -L $my_top_dir/prebuilts/kernel-build-tools/linux-x86/lib64 -fuse-ld=lld --rtlib=compiler-rt" KCFLAGS="${KCFLAGS} -D__ANDROID_COMMON_KERNEL__"

mkdir -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist

mkdir -p $my_top_dir/out/msm-kernel-kalama-gki/msm-kernel $my_top_dir/out/msm-kernel-kalama-gki/dist

cd $my_top_dir/common 

make -j$(nproc) O=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common gki_defconfig

make -j$(nproc) O=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common olddefconfig

make -j$(nproc) O=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common  

make -j$(nproc) O=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common INSTALL_MOD_PATH=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/staging  modules_install

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/arch/arm64/boot/Image $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/vmlinux $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/System.map $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/vmlinux.symvers $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/modules.builtin $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/modules.builtin.modinfo $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/arch/arm64/boot/Image.lz4 $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/common/arch/arm64/boot/Image.gz $my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist/

MAKE_ARGS="KBUILD_MIXED_TREE=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist"

cd $my_top_dir/external/dtc

make -j$(nproc) all install CC=clang AR=llvm-ar LDFLAGS="--sysroot=$my_top_dir/build/kernel/build-tools/sysroot  -Wl,-rpath,$my_top_dir/prebuilts/kernel-build-tools/linux-x86/lib64 -L $my_top_dir/prebuilts/kernel-build-tools/linux-x86/lib64 -fuse-ld=lld --rtlib=compiler-rt -fuse-ld=lld --rtlib=compiler-rt" EXTRA_CFLAGS="--sysroot=$my_top_dir/build/kernel/build-tools/sysroot  -I$my_top_dir/prebuilts/kernel-build-tools/linux-x86/include" PKG_CONFIG=false NO_PYTHON=1 PREFIX=$my_top_dir/out/msm-kernel-kalama-gki/host 

cd $my_top_dir

KCONFIG_CONFIG=./msm-kernel/arch/arm64/configs/vendor/kalama-gki_defconfig ./msm-kernel/scripts/kconfig/merge_config.sh -m -r -y ./msm-kernel/arch/arm64/configs/gki_defconfig ./msm-kernel/arch/arm64/configs/vendor/kalama_GKI.config ./msm-kernel/arch/arm64/configs/vendor/ext_config/moto-kalama.config ./msm-kernel/arch/arm64/configs/vendor/ext_config/moto-kalama-rtwo.config ./msm-kernel/arch/arm64/configs/vendor/ext_config/moto-kalama-gki.config

cd $my_top_dir/msm-kernel

make -j$(nproc) LLVM=1 DEPMOD=depmod DTC=$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc O=$my_top_dir/out/msm-kernel-kalama-gki/msm-kernel KBUILD_MIXED_TREE=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist vendor/kalama-gki_defconfig

make -j$(nproc) O=$my_top_dir/out/msm-kernel-kalama-gki/msm-kernel LLVM=1 DEPMOD=depmod DTC=$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc KBUILD_MIXED_TREE=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist modules dtbs

make -j$(nproc) O=$my_top_dir/out/msm-kernel-kalama-gki/msm-kernel LLVM=1 DEPMOD=depmod DTC=$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc  INSTALL_MOD_PATH=$my_top_dir/out/msm-kernel-kalama-gki/staging KBUILD_MIXED_TREE=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist modules_install

cp -p $my_top_dir/out/msm-kernel-kalama-gki/msm-kernel/.config $my_top_dir/out/msm-kernel-kalama-gki/dist/

cp -p $my_top_dir/out/msm-kernel-kalama-gki/msm-kernel/Module.symvers $my_top_dir/out/msm-kernel-kalama-gki/dist/

make -j$(nproc) -C $my_top_dir/out/msm-kernel-kalama-gki/msm-kernel O=$my_top_dir/out/msm-kernel-kalama-gki/msm-kernel LLVM=1 DEPMOD=depmod DTC=$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc INSTALL_HDR_PATH=$my_top_dir/out/msm-kernel-kalama-gki/kernel_uapi_headers/usr KBUILD_MIXED_TREE=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist headers_install

make -j$(nproc) LLVM=1 DEPMOD=depmod DTC=$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc O=$my_top_dir/out/msm-kernel-kalama-gki/msm-kernel KBUILD_MIXED_TREE=$my_top_dir/out/msm-kernel-kalama-gki/gki_kernel/dist INSTALL_DTBS_PATH=$my_top_dir/out/msm-kernel-kalama-gki/dtb_staging DTB_TYPES=kalama-overlays- dtbs_install
```

## WLAN Driver

```bash
cd $my_top_dir 

make -j$(nproc) -C ..//vendor/qcom/opensource/wlan/qcacld-3.0/.kiwi_v2 M=../../vendor/qcom/opensource/wlan/qcacld-3.0/.kiwi_v2 KERNEL_SRC=$my_top_dir/./msm-kernel O=$my_top_dir/out/msm-kernel-kalama-gki/msm-kernel LLVM=1 DEPMOD=depmod DTC=$my_top_dir/build/kernel/build-tools/path/linux-x86/dtc WLAN_ROOT=vendor/qcom/opensource/wlan/qcacld-3.0/.kiwi_v2 WLAN_COMMON_ROOT=cmn WLAN_COMMON_INC=vendor/qcom/opensource/wlan/qcacld-3.0/cmn WLAN_FW_API=vendor/qcom/opensource/wlan/fw-api WLAN_PROFILE=kiwi_v2 DYNAMIC_SINGLE_CHIP= MODNAME=kiwi_v2 DEVNAME=kiwi_v2 BOARD_PLATFORM=kalama CONFIG_QCA_CLD_WLAN=m WLAN_CTRL_NAME=wlan CONFIG_CNSS_OUT_OF_TREE=y CONFIG_CNSS2=m CONFIG_CNSS2_QMI=y CONFIG_CNSS_QMI_SVC=m CONFIG_CNSS_PLAT_IPC_QMI_SVC=m CONFIG_CNSS_GENL=m CONFIG_WCNSS_MEM_PRE_ALLOC=m CONFIG_CNSS_UTILS=m CONFIG_BUS_AUTO_SUSPEND=y CONFIG_CNSS_HW_SECURE_DISABLE=y KERNEL_SUPPORTS_NESTED_COMPOSITES=n KBUILD_EXTRA_SYMBOLS=$my_top_dir/../vendor/qcom/opensource/wlan/qcacld-3.0/Module.symvers ANDROID_BUILD_TOP=$my_top_dir/.. KBUILD_MIXED_TREE=out/msm-kernel-kalama-gki/msm-kernel
```

## Minimal requirements to compile the Kernel

* [source](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-T1RA33.55-15-10/Documentation/process/changes.rst)

```rest
====================== ===============  ========================================
        Program        Minimal version       Command to check the version
====================== ===============  ========================================
GNU C                  4.6              gcc --version
GNU make               3.81             make --version
binutils               2.20             ld -v
flex                   2.5.35           flex --version
bison                  2.0              bison --version
util-linux             2.10o            fdformat --version
kmod                   13               depmod -V
e2fsprogs              1.41.4           e2fsck -V
jfsutils               1.1.3            fsck.jfs -V
reiserfsprogs          3.6.3            reiserfsck -V
xfsprogs               2.6.0            xfs_db -V
squashfs-tools         4.0              mksquashfs -version
btrfs-progs            0.18             btrfsck
pcmciautils            004              pccardctl -V
quota-tools            3.09             quota -V
PPP                    2.4.0            pppd --version
isdn4k-utils           3.1pre1          isdnctrl 2>&1|grep version
nfs-utils              1.0.5            showmount --version
procps                 3.2.0            ps --version
oprofile               0.9              oprofiled --version
udev                   081              udevd --version
grub                   0.93             grub --version || grub-install --version
mcelog                 0.6              mcelog --version
iptables               1.4.2            iptables -V
openssl & libcrypto    1.0.0            openssl version
bc                     1.06.95          bc --version
Sphinx                 1.3              sphinx-build --version
====================== ===============  ========================================
```

* `Sphinx` is needed only to build the Kernel documentation