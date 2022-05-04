# fio_configs
Some fio config files for testing

fio is a tool used to test system i/o capacity. See https://fio.readthedocs.io/en/latest/ for more information.

## Usage

Pre-populate a file, perhaps mounted on an attached disk.

`fio --section=populate populate.cfg`

Run the suite of tests.

`fio --output=fio.log fio.cfg`

Example of running just one test.

`fio --section=write-latency --output=fio_write_latency.log fio.cfg`

Generate graphs.

`fio_generate_plots "Your Title Here"`

Alternatively, look for values exceeding a certain level. This example shows the count of write latency entries over 10ms.

`cat 4k-write-latency.results_lat.1.log | awk -F',' '$2>10000000 {print ;}' | wc -l`

Note: The fio version installed from at least the Centos 7 packages is quite old. Here are some example steps to installing the latest fio version.

```
yum install screen git gcc-c++ svn texinfo-tex flex zip libgcc.i686 glibc-devel.i686 zlib-devel

screen
svn co svn://gcc.gnu.org/svn/gcc/tags/gcc_9_2_0_release/
cd gcc_9_2_0_release/
./contrib/download_prerequisites
cd ..
mkdir gcc_9_2_0_release-build
cd gcc_9_2_0_release-build/

../gcc_9_2_0_release/configure && make -j 16 && sudo make install && echo "finished"
```
