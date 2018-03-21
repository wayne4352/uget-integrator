# uGet Integrator

Integrate uGet Download Manager with Google Chrome, Chromium, Opera, Vivaldi and Mozilla Firefox.

## Installation

> After installing `uget-integrator`, install [uget-extension](https://github.com/ugetdm/uget-extension) and restart your browser.

### Arch

```
pacaur -S uget-integrator-chrome uget-integrator-chromium uget-integrator-opera uget-integrator-firefox
```

> Vivaldi users must install `uget-integrator-chromium`

Above packages bind `uget-integrator` with respective browsers. You can ignore a package if you do not have the browser or do not want to integrate it with uGet.

For example, if you use Mozilla Firefox only, installing `uget-integrator-firefox` is enough.

### Ubuntu & Linux Mint

```
sudo add-apt-repository ppa:uget-team/ppa
sudo apt update
sudo apt install uget-integrator
```

### Other Linux

```
wget https://raw.githubusercontent.com/ugetdm/uget-integrator/master/install/linux/install_uget_integrator.sh
sudo sh install_uget_integrator.sh
```

### Windows

#### Recommended Method

1. Install the latest uGet Download Manager using [Windows installer](https://github.com/ugetdm/uget-windows-installer/releases)
2. Download and install the latest [uget-integrator_x.x.x.x.exe](https://github.com/ugetdm/uget-integrator/releases)

#### Portable Method

> **Note: Portable method involves manual configurations so it is only recommended for advanced users**

1. Download and extract portable uGet Download Manager from [official website](http://www.ugetdm.com/downloads-windows)
2. Download and extract the latest [uget-integrator_win_x.x.x.zip](https://github.com/ugetdm/uget-integrator/releases)
3. Open `uget-integrator\uget-integrator.py` in Notepad and replace `"C:\\uGet\\bin\\uget.exe"` in [line no 38](https://github.com/ugetdm/uget-integrator/blob/master/bin/uget-integrator#L38) by the absolute path of `uget.exe`
    Suppose you extracted uGet into `C:\Program Files (x86)` directory then line no 38 should look like this:
    ```python
    UGET_COMMAND = "C:\\Program Files (x86)\\uGet\\bin\\uget.exe"
    ```
    > Note that `\\` is used in place of `\`

    Relative path should work without any problems. However, we recommend to use relative paths in the following format to avoid *unexpected* runtime problems. In this format, you need to replace `"..\\uGet\\bin\\uget.exe"` by the actual relative path of `uget.exe`.
    ```python
    UGET_COMMAND = join(os.path.dirname(os.path.realpath(__file__)), "..\\uGet\\bin\\uget.exe")
    ```
    Above example assumes the following folder structure:
    ```
    .
    |- uget-integrator
        |- add_config.bat
        |- LICENSE
        |- remove_config.bat
        |- uget-integrator.bat
        |- uget-integrator.py
        |- python-3.6.4
    |- uGet
        |- bin
            |- uget.exe
            |- other files
        |- other files and folders
    ```
4. Execute `uget-integrator\add_config.bat` to create required configuration files and Registry entries

## Known Issues

**Firefox not interrupting downloads**
If the uGet extension does not interrupt downloads in Mozilla Firefox, first ensure that the architecture(`32` bit or `64`bit) of Firefox match with your operating system.
If that does not help, delete `handlers.json` from the following path:

Firefox Stable:
```
~/.mozilla/firefox/mwad0hks.default/handlers.json
```

Firefox Nightly:
```
~/.mozilla/firefox-trunk/mwad0hks.default/handlers.json
```

Where `mwad0hks` is a random string so you may have a different folder name.

If the above solution works but does not persist, solution provided in [#3](https://github.com/ugetdm/uget-integrator/issues/3) may give you a permanent solution.

For more details, please check issues [#43](https://github.com/slgobinath/uget-chrome-wrapper/issues/43) and [#3](https://github.com/ugetdm/uget-integrator/issues/3).


## Build Packages

These commands are only for the developer to automate package creations.
```bash
mkdir build
cd build
rm -rf *; cmake ..; make deb_package zip_package nsis_package
```

## License

GNU General Public License v3