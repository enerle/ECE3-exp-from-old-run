# ECE3-exp-from-old-run-
launching new EC-Earth3 experiment from old run 

    . module_list.sh 
    module load Mambaforge/23.3.1-1-hpc1 
    mamba activate ecearth

Run configuration file
    util/ec-conf/ec-conf3 -p nsc-tetralith-el9-intel-intelmpi config-build.xml

**Compiling Oasis**

    cd oasis3-mct-5.2/util/make_dir/
    make -f Makefile.ece realclean
    make -f Makefile.ece pyoasis

**Compiling XIOS**

    cd xios-2.5/
    ./make_xios --arch ecconf --use_oasis oasis3_mct --netcdf_lib netcdf4_par  --job 6

**Compiling NEMO**
