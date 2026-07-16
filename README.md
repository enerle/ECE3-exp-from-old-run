# ECE3-exp-from-old-run-

Launching new EC-Earth3 experiment from old run 

1. Create a new run-script

    cp the old run-script or generate a new with ec-conf

2. Create a new run-script: copy the old run-script or generate a new with ec-conf.
   Change exp_name to a new name, keep run_start_date (important!) but adjust run_end_date, forcing, etc for your new experiment.

Keep numproc as in the old run-script

Execute the new run-script from the command line (not sbatch) to get a fresh run_dir with exectuables and many other files.
Once you have come that far you can start filling the new run_dir with restart files from the old run. "Leg" in the following denotes the leg number when your experiment starts. Note that some files have to be copied while others can be linked (or copied if you prefer)

        cp ece.info new run_dir

edit this file so that the last entry contains only the lines up to the year _before_ your new run starts (e.g. if you plan to start at leg=201 you should delete all entries with leg>= 201, the last entry in ece.info would be for leg=200)

       cd new run_dir
       cp old_run_dir/restart/ifs/leg/rcf .
       ln -s old_run_dir/restart/ifs/leg/srf* .
       ln -s old_run_dir/restart/nemo/leg/* .
       ln -s old_run_dir/restart/oasis/leg/* .  ###??restart/oasis
       mkdir -p restart/{oasis,lpjg} 

Are you running with PISCES?
        
        ln -s old_run_dir/log/leg-1/ocean.carbon to your new_run_dir

Are your running with LPJG?
        
        cp -R old_run_dir/restart/lpjg/leg-1  new_run_dir/restart/lpjg
        ln -s old_run_dir/restart/oasis/leg-1 new_run_dir/restart/oasis

Are you running with co2box?
        
        cp old_run_dir/restart/co2box/leg-1/* new_run_dir

Are you running with PISM?

    mkdir new_run_dir/pism_grtes/pism_YYYY  #where YYYY is the year just _before_ your new experiment is supposed to start
    cp old_run_dir/restart/pism_grtes/leg/* new_run_dir/pism_grtes/pism_YYYY

Are you running with fwf?

        cp old_run_dir/restart/fwf/leg/* new_run_dir/fwf/interactive/forcing_files/        
        ln -s fwf/interactive/forcing_files/ FWF_LRF_yYYYY.nc new_run_dir/freshwater_forcing_yYYYY.nc  #where yYYYY is the year when your new experiment starts. Note the "y" in front of the year, e.g. y2100.

Submit a 1-yr job and see if everything works fine. PISM and FWF are run after the first year has finished so you have to wait to be sure that they work fine, too.

delete:
        rm -f restart_{oce,ice,trc}.nc
