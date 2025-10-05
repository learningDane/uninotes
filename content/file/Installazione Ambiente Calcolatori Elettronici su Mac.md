#uni 
# LIBCE
```bash
brew install make x86_64-elf-gcc x86_64-elf-gdb wget
	#GNU "make" has been installed as "gmake".
	#If you need to use it as "make", you can add a "gnubin" directory
	#to your PATH from your bashrc like:
	#PATH="/opt/homebrew/opt/make/libexec/gnubin:$PATH"
wget https://calcolatori.iet.unipi.it/resources/libce-4.3.tar.gz
tar xvzf libce-4.3.tar.gz
cd libce-4.3
make
make install
	#==> Creo '/Users/davidesqueri/CE/share/hd.img' (dimensione: 20M)
	#==> Installo libce.conf in '/Users/davidesqueri/CE/etc'
	#==> Installo libce64.a e libce-debug.py in '/Users/davidesqueri/CE/lib64/ce'
	#==> Installo i file .h in '/Users/davidesqueri/CE/include/ce'
	#==> Installo boot.bin e boot.ld in '/Users/davidesqueri/CE/lib/ce'
	#==> Installo gli script in '/Users/davidesqueri/CE/bin'
echo $HOME/CE/bin | sudo tee -a /etc/paths
	#aggiunge boot compile e debug al path
```
# QEMU
```bash
python3 -m pip install tomli
brew install coreutils
echo 'export PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"' >> ~/.zshrc
# poi ricaricare la shell:
source ~/.zshrc
brew install ninja pkg-config sphinx-doc glib
wget https://calcolatori.iet.unipi.it/resources/qemu-ce-9.2.2-3.tar.gz
tar xvf qemu-ce-9.2.2-3.tar.gz
cd qemu-ce-9.2.2-3
./install
```
# Nucleo
```bash
# scaricare cartella dove volete
# scompattare:
tar xvf nucleo-8.3.tar.gz
```

> informazioni sull'uso di [[LIBCE]], esempiIO e nucleo: [[Comandi Utili Calcolatori Elettronici]]

