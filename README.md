### Creating a Singularity container for [TurboSETI](https://github.com/UCBerkeleySETI/turbo_seti) and dependencies

For an introduction to Singularity, please see the [documentation](https://sylabs.io/guides/3.5/user-guide/introduction.html).  

To install Singularity, please see the [installation guide](https://sylabs.io/guides/3.0/user-guide/installation.html).  

A Singularity container can be built from a [definition file](https://sylabs.io/guides/3.5/user-guide/definition_files.html). A definitions file for TurboSETI is given by [`turboseti_container.def`](turboseti_container.def). The following command will create a TurboSETI container named `turboseti_container.sif`:

```
sudo singularity build turboseti_container.sif turboseti_container.def   
```

Note that the CUDA drivers on the host system must be compatible with the CUDA toolkit version installed in the container (as specified in the definitions file). This can be confirmed by checking the [compatibility table](https://docs.nvidia.com/deploy/cuda-compatibility/index.html) (Table 2 in the document linked).

The container can be accessed via a shell as follows:  

```
singularity shell --nv turboseti_container.sif
```

The `--nv` flag is needed for GPU support. In addition, one may wish to make external directories available within the container. This can be achieved using the `-B` or `--bind` flags as follows:  

```
singularity shell -B ~/example_data --nv turboseti_container.sif
```

TurboSETI may also be run from within the container via the external commandline as follows:  

```
singularity exec -B ~/example_data --nv turboseti_container.sif turboSETI ~/example_data/diced_Parkes_57941_12846_HIP33499_S_fine.h5 -g y
```
