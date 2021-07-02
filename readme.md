# Solution

Read this comment:
https://github.com/conda/conda-build/issues/4188#issuecomment-853712188

# Problem description

I built a package using `conda build` but I cannot import the installed module. The build process finishes without any (visible?) issues and I can install it (`conda list` shows that it is installed) but when I try to import the module I get a `No module named condamwe` error.

This repository shows a Minimal Working Example (MWE) in the hope that someone can help me figure out what is the issue :)

# Building the package

Once you downloaded the repository go to the `condamwe` folder (`cd condamwe`). Then run `conda build . --output-folder ../builds`. This will build the package and put the contents to the `builds` folder.

The two following warnings popup but I have no idea whether they are important and how to fix them:
```
WARNING:conda_build.build:No files or script found for output condamwe
WARNING conda_build.build:bundle_conda(1553): No files or script found for output condamwe
```

# Installation

Run `conda install ../builds/linux-64/condamwe-1.0.0-0.tar.bz2` to install it.

Using `conda list | grep "condamwe"` should return one line which shows that the package is installed.

# Run the example code

In the root folder I put two code examples `example_run.py` and `example_run_local_pkg.py`. First try to run `python example_run_local_pkg.py`, this should give you "42" as the output. It only works because python looks up the package in one of the subfolders.

If you run `python example_run.py`, it should give you the following error: `ImportError: cannot import name 'mwe' from 'condamwe' (unknown location)`

# Things I tried and other useful info
- This is just an MWE but I tried more complex `meta.yml` files. It installed dependencies etc but the module was not available anyway. Only the name should be required based on: `https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html`
- Using a build file/filling in the build section of the meta file did not help
- I was able to create and install pip packages
