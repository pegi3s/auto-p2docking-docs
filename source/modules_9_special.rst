Special
*******

split
-----

This is a special command, that is invoked after a regular command, and that takes as input a single argument, namely, the number of groups to consider. For instance, the instruction: "CGF_and_CGA_CDS_processing my_data_dir out_dir split 20" will split the files that are in the my_data_dir directory into 20 equal size subfolders. The data on each subfolder will be processed independently, thus avoiding out of memory errors. The output of all independent analyses will be saved in the out_dir directory.