# Deblint

Deblint is a tool for tracking down unused Debian packages that no other packages depend on. It's designed to help you clean up your system by identifying and removing packages that are no longer needed.

Deblint uses atime to decide which packages have not been used in the set time, the default is 7 days.

## Usage

```deblint <days> (default=7)```

## Features

- Identifies unused Debian packages that no other packages depend on.
- Provides a whitelist feature to exclude certain packages from being suggested for removal.
- Clean and easy-to-understand output.

## Recent Updates

- Added support for a whitelist of packages not to uninstall: You can now specify a list of packages that should not be suggested for removal, even if they are not used by any other packages.

## Whitelist

To use the whitelist feature, create a newline-separated list of package names in a file called `/etc/deblint/whitelist`. These packages will be excluded from the list of packages suggested for removal.

For example:

```
init
debian-keyring
dns-root-data
firmware-linux
firmware-linux-nonfree
```

## Building a Debian Package

To build a Debian package of this project, follow these steps:

1. Install the necessary build dependencies:

    ```bash
    sudo apt-get install devscripts debhelper
    ```

2. Navigate to your project directory:

    ```bash
    cd /path/to/your/project
    ```

3. Create a source tarball in the parent directory of your project:

    ```bash
    tar czvf ../deblint_0.0.0.orig.tar.gz .
    ```

    Replace `0.0.0` with your actual package version.

4. Build the Debian package:

    ```bash
    debuild -us -uc
    ```

    This command will create a `.deb` file in the parent directory of your project.

5. To install the package, use the `dpkg` command:

    ```bash
    sudo dpkg -i ../your-package-name.deb
    ```

* To increment the version of your package, run:

    ```bash
    dch -i
    ```

## Testing

To change the atime of the files belonging to a package 
you can run something like this:
```
export DATE=$(date -d "7 days ago" +%Y%m%d%H%M)
for file in `dpkg -L cowsay` ; do sudo touch -a -t $DATE $file; done
```
