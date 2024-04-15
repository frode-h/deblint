# Deblint

Deblint is a tool for tracking down unused Debian packages that no other packages depend on. It's designed to help you clean up your system by identifying and removing packages that are no longer needed.

Deblint uses atime to decide which packages have not been used in the set time, the default is 7 days.

## Usage

deblint <days> (default=7)

## Features

- Identifies unused Debian packages that no other packages depend on.
- Provides a whitelist feature to exclude certain packages from being suggested for removal.
- Clean and easy-to-understand output.

## Recent Updates

In the recent update, the following enhancements were made:

- Added support for a whitelist of packages not to uninstall: You can now specify a list of packages that should not be suggested for removal, even if they are not used by any other packages.

## Whitelist

To use the whitelist feature, create a newline-separated list of package names in a file called `/etc/deblint/whitelist`. These packages will be excluded from the list of packages suggested for removal.

For example:
/etc/deblint/whitelist:
init
debian-keyring
dns-root-data
firmware-linux
firmware-linux-nonfree
