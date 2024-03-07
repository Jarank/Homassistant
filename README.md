# Homassistant
https://github.com/home-assistant/supervised-installer
-------------------------------------------------------------------------------------------------------

https://community.home-assistant.io/t/install-home-assistant-os-with-kvm-on-ubuntu-headless-cli-only/254941
# step
apt install -y qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils ovmf virt-manager
egrep -c '(vmx|svm)' /proc/cpuinfo

virsh pool-create-as --name VMS --type dir --target /var/lib/libvirt/images/hassos-vm
cd /var/lib/libvirt/images/hassos-vm
xz -d -v haos_ova-11.5.qcow2.xz

virt-install --import --name hass --memory 2048 --vcpus 2 --cpu host --disk haos_ova-11.5.qcow2,format=qcow2,bus=virtio --network bridge=br0,model=virtio --osinfo detect=on,require=off --graphics none --noautoconsole --boot uefi
