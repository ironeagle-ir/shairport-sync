At the time of writing, the Raspbian image `2015-01-31-raspbian` does not include `libsoxr`, not is it available as a package via `apt-get`.
It is, however, easy to compile, and works well with Shairport Sync on the Raspberry Pi. Here are very brief instructions to download, compile and install it so that it can be used with Shairport Sync.

* Install `cmake`. This is used in the building of libsoxr:
```
sudo apt-get install cmake
```
* Download the `libsoxr source`:
```
git clone git://git.code.sf.net/p/soxr/code libsoxr
```
* `cd` into the `libsoxr` directory and start the build process:
```
cd libsoxr
./go
```
Be patient! This takes a long time on a Raspberry Pi -- it looks like it gets stuck at 47%, but it will finish if you let it.
* Next `libsoxr` must be installed:
```
cd Release
sudo make install
```
Finally, for Shairport Sync to be able to locate `libsoxr-dev` during compilation, you need to tell `ld` where to find it:
```
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
export LD_LIBRARY_PATH
sudo ldconfig -v
```
That's it. Now you can select the `--with-libsoxr` option when you're building Shairport Sync