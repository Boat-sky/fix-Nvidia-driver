# fix-Nvidia-driver
1. เปิดหน้า Gui แล้วเลือกเวอร์ชั่น driver ที่แนะนำ (กรณีเป็น 435)
2. หาทำข้อ 1. ไม่ได้ อาจจะเพราะว่ามีบางอย่งที่ค้างอยู่ ลอง   
```
LC_MESSAGES=C dpkg-divert --list '*nvidia-340*' | sed -nre 's/^diversion of (.*) to .*/\1/p' | xargs -rd'\n' -n1 -- sudo dpkg-divert --remove
sudo apt --fix-broken install
```
ดูเพิ่มเติมได้ที่ https://askubuntu.com/questions/1035409/installing-nvidia-drivers-on-18-04   
3. ถ้ทำข้อ 1 ได้ต่อไป
```
sudo apt-get purge nvidia*
Reboot
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo apt-get install nvidia-driver-435
Reboot
```
4. หากมีการแจ้งเตอนว่า Possible missing firemware ลอง เข้าลิงค์นี้ http://anduin.linuxfromscratch.org/sources/linux-firmware/i915/ และโหลดตัวที่ขาด แล้ว coppy มาวางมที่ /lib/firmware/i915/
แล้วสั่ง `sudo apt-get update -y`   
ดูเพิ่มเติมได้ที่ https://unix.stackexchange.com/questions/556946/possible-missing-firmware-lib-firmware-i915-for-module-i915/556947#556947   

5. เรียกการใช้งาน nvidia ด้วย
```
sudo prime-select nvidia
```   
ถ้าขึ้นว่า  Info: the nvidia profile is alreadt set แสดงว่าใช้งานได้แล้ว   
6. ใช้คำสั่ง
```
sudo update-initramfs -u
```
7. 
```
sudo ubuntu-drivers devices
sudo ubuntu-drivers autoinstall
sudo reboot
```
ข้อ 5-7 สามารถดูเพิ่มเติมได้ที่ https://forums.developer.nvidia.com/t/newly-installed-drivers-are-not-found-when-nvidia-smi-is-called/82686
