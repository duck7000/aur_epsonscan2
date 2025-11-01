
This repo is for patching epsonscan2 to work on Arch based Linux. De standard AUR version misses a important patch that prohibite epsonscan to even open or find a connected scanner.

    First install all depencys:
    yay -S libjpeg-turbo libpng libtiff libusb qt5-base sane zlib boost cmake qt5-singlecoreapplication rapidjson bbe
    
    git clone https://github.com/duck7000/aur_epsonscan2.git

    cd aur_epsonscan2

    makepkg -si

    Install epsonscan2 non free plugin (it should be needed only for wireless scanning and pdf but my V330 will not work without it
    yay epsonscan2-non-free-plugin
