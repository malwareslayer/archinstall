# archlinux-install
My Boilerplate Setup With Tweak &amp; Config Archlinux Installer

### ext4

```
mkfs.ext4 -O fast_commit,metadata_csum,encrypt /dev/X/Y
```

Note: Don't use fscrypt (encrypt) if you don't need it and change homed.conf `DefaultStorage=storage`

### fstab

```
# tweak user options: rw,relatime,journal_checksum,delalloc,data=ordered

tmpfs				/tmp		tmpfs	rw,nodev,nosuid,size=4G 0 0

tmpfs				/run		tmpfs	rw,nodev,nosuid,size=4G 0 0

/tmp                            /var/tmp        none	rw,nodev,nosuid,bind 0 0

/run				/var/run	none	rw,nodev,nosuid,bind 0 0

tmpfs				/dev/shm	tmpfs	rw,size=4G 0 0
```

### user

```
homectl update <username> \
    --setenv="PATH=$PATH:$HOME/.local/bin" \
    
    --setenv="XDG_CONFIG_HOME=$HOME/.config" \
    --setenv="XDG_DATA_HOME=$HOME/.local/share" \
    --setenv="XDG_STATE_HOME=$HOME/.local/state" \
    --setenv="XDG_CACHE_HOME=$HOME/.cache" \
    --setenv="XDG_RUNTIME_DIR=/run/user/$(id -u $USER)" \
    
    --setenv="GOCACHE=$XDG_CACHE_HOME/go/build" \
    --setenv="GOMODCACHE=$XDG_CACHE_HOME/go/pkg/mod" \
    --setenv="GOPATH=$XDG_DATA_HOME/go" \
    
    --setenv="ANDROID_HOME=$HOME/Android" \
    
    --setenv="MOZ_ENABLE_WAYLAND=1" \
    --setenv="GDK_BACKEND=wayland,x11" \
    --setenv="QT_QPA_PLATFORM=wayland;xcb" \
    --setenv="QT_QPA_PLATFORMTHEME=gtk4" \
    --setenv="QT_AUTO_SCREEN_SCALE_FACTOR=1" \
    
    --setenv="LIBVA_DRIVER_NAME=radeonsi" \
    --setenv="VDPAU_DRIVER=radeonsi" \
    --setenv="__GLX_VENDOR_LIBRARY_NAME=amd" \
    --setenv="AMD_VULKAN_ICD=RADV" \
    --setenv="DISABLE_LAYER_AMD_SWITCHABLE_GRAPHICS_1=1" \
    --setenv="VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/radeon_icd.i686.json:/usr/share/vulkan/icd.d/radeon_icd.x86_64.json"
```