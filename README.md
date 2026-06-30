# auriga-tutorial-toronto2026

Created by Alex Riley (for better or worse), built off of Rob Grand's `auriga_public` and `SimulationsTutorial.ipynb`.

# Initial set up

In order to analyse publicly available Auriga data ([Grand+2024](https://scixplorer.org/abs/2024MNRAS.532.1814G/abstract)), you will need to
* create a Python environment (or adapt one you already own)
* download the Auriga data via Globus

## Python environment

There's a `conda-env.yml` file in this repo that specifies the packages you need. There a usual mix of `numpy`/`scipy`/`matplotlib` and similar packages. The ones that are non-standard are:
* `h5py` - Python interface for the HDF5 binary data format
* `auriga_public` - lightweight Python scripts for loading and analysing Auriga data available [on BitBucket](https://bitbucket.org/grandrt/auriga_public/src/master/). This can be `pip` installed
* `cmasher` - for good colormaps

If you want an easy life, just run `conda create -f conda-env.yml`, which will create a conda environment named `auriga` that has everything you need. This will include running `pip install` to get `auriga_public`, using this conda environment's `pip` for minimal contamination.

## Downloading Auriga
For this tutorial, you will download the Auriga snapshots locally to your machine. You only need the present-day snapshots ("redshift zero") of the level 4 runs of Au-6 and Au-18, along with the merger trees and "accreted particle lists" for those haloes. This will require ~7 GB of disk storage (if this is a challenge, you can opt for only Au-6 which is ~2.7 GB).

If you want to download other haloes, earlier snapshots, and/or higher resolution runs, the process is similar to the instructions below.

### Setting up Globus

[Globus](https://www.globus.org/) is a file transfer service built to move, share, and archive large datasets (tera- or peta-bytes, plus).

The key setup steps for this tutorial:
* Create a login account, either directly with Globus or using your institutional account
* Download [Globus Connect Personal](https://www.globus.org/globus-connect-personal) to make your laptop an endpoint

Here's a [useful tutorial](https://docs.globus.org/guides/tutorials/manage-files/transfer-files/) to have open as you're doing the next steps (this walks through a dummy transfer).

### Auriga on Globus

The Auriga data are available at the following endpoint:
* Globus ID: [02a2dbb8-f64d-4440-bafe-44b60b964501](https://app.globus.org/file-manager?origin_id=02a2dbb8-f64d-4440-bafe-44b60b964501&origin_path=%2F)
* Display name: The Auriga Simulations

For this tutorial, you want to transfer the content of the the following folders to your machine:
```
level4
    Original
        halo_6
            groups_127
            snapdir_127
        halo_18
            groups_127
            snapdir_127
        lists
            accretedstardata
                halo_6
                halo_18
        mergertrees
            halo_6
            halo_18
```

This will download the halo catalogues (`groups`) and particle data (`snapdir`) for the final snapshot (`127`), as well as the accreted particle lists (`accretedstardata`) and merger trees (`mergertrees`).

On my machine I simplify the file structure a little bit so it looks like the following:
```
level4
    halo_6
        groups_127
        snapdir_127
    halo_18
        groups_127
        snapdir_127
    accretedstardata
        halo_6
        halo_18
    mergertrees
        halo_6
        halo_18
 ```
