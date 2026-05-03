
This repo is for patching epsonscan2 to work on Arch based Linux.
De standard AUR version misses a important patch that prohibite some scanners to even open or finding a connected scanner

Changelog:<br>
Updated to version 6.7.87.0<br>
Updated to version 6.7.82.0

First install all depencencies:<br>
yay -S libjpeg-turbo libpng libtiff libusb qt5-base sane zlib boost cmake qt5-singlecoreapplication rapidjson bbe libharu
    
git clone https://github.com/duck7000/aur_epsonscan2.git

cd aur_epsonscan2

makepkg -si

Install epsonscan2 non free plugin:<br>
yay epsonscan2-non-free-plugin

The non free plugin is not only for OCR or Wireless scanning, some models do need a proprietary firmware!
Here is a list of models that need firmware, get the device id through lsusb

ATTRS{idProduct}=="0130", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw7c.bin"<br>
ATTRS{idProduct}=="0133", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw86.bin"<br>
ATTRS{idProduct}=="013a", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfwa1.bin"<br>
ATTRS{idProduct}=="013b", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfweb.bin"<br>
ATTRS{idProduct}=="013c", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw010c.bin"<br>
ATTRS{idProduct}=="013d", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw010c.bin"<br>
ATTRS{idProduct}=="013e", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw0282.bin"<br>
ATTRS{idProduct}=="013f", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw0282.bin"<br>
ATTRS{idProduct}=="0142", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfwad.bin" (V330)<br>
ATTRS{idProduct}=="014a", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfwdd.bin"<br>
ATTRS{idProduct}=="0153", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw0111.bin"<br>


    Perfection V600 / GT-X820                    (idProduct=="013a")
    
    Perfection V550                              (idProduct=="013b")
    
    Perfection V19                               (idProduct=="013c")
    
    Perfection V39 / GT-S650                     (idProduct=="013d")
    
    Perfection V37/V370/GT-S640/F740             (idProduct=="014a")
    
    Perfection V33 / V330 / GT-S630 / GT-F730    (idProduct=="0142")
    
    Perfection V19II                             (Unknown)
    
    Perfection V39II / GT-S660                   (idProduct=="013f")
    
    Perfection V500 / GT-X770                    (Unknown)
    
    WorkForce GT-1500 / GT-D1000                 (Unknown)
    
    DS-5500/DS-6500/DS-7500                      (idProduct=="0x145")
    
    DS-50000/DS-60000/DS-70000                   (idProduct=="0x146")
    
    GT-X830                                      (Unknown)

