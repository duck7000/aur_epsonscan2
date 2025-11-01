
This repo is for patching epsonscan2 to work on Arch based Linux. De standard AUR version misses a important patch that prohibite epsonscan to even open or find a connected scanner.

    First install all depencys:
    yay -S libjpeg-turbo libpng libtiff libusb qt5-base sane zlib boost cmake qt5-singlecoreapplication rapidjson bbe
    
    git clone https://github.com/duck7000/aur_epsonscan2.git

    cd aur_epsonscan2

    makepkg -si

    Install epsonscan2 non free plugin
    yay epsonscan2-non-free-plugin

The non free plugin is not only for OCR or Wireless scanning, some models do need a proprietary firmware!
Here is a list of models that need firmware, get the device id through lsusb

ATTRS{idProduct}=="0130", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw7c.bin"<br>
ATTRS{idProduct}=="0133", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw86.bin"<br>
ATTRS{idProduct}=="013a", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfwa1.bin"<br>
ATTRS{idProduct}=="013b", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfweb.bin"<br>
ATTRS{idProduct}=="013c", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw010c.bin"<br>
ATTRS{idProduct}=="013c", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw010c.bin"<br>
ATTRS{idProduct}=="013d", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw010c.bin"<br>
ATTRS{idProduct}=="013e", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw0282.bin"<br>
ATTRS{idProduct}=="013f", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw0282.bin"<br>
ATTRS{idProduct}=="0142", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfwad.bin" (V330)<br>
ATTRS{idProduct}=="014a", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfwdd.bin"<br>
ATTRS{idProduct}=="0153", ENV{epsonscan2_driver}="esci", ENV{firmware_file}="esfw0111.bin"<br>
