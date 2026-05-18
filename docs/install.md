# Installing pySNOW

The first step (suggested) is to create a python environment for installation to avoid confilcts with previously installed libraries or different versions of required modules, e.g.:

=== "Linux"

    ```bash
    python3 -m venv snowenv
    source snowenv/bin/activate
    ```

=== "Mac"

    ```bash
    python3 -m venv snowenv
    source snowenv/bin/activate
    ```

=== "Windows"

    ```bash
    python -m venv snowenv
    .\snowenv\Scripts\activate
    ```
Note that `pySNOW` requires a version of python >= 3.9, however users can optionally try to change this in the **pyproject.toml** file, this however has not been tried and might result in unwanted behaviour. Going below python 3 is sure to cause issues due to syntax differences.

After creating and activating the virtual environment you can clone the repository (or download the code as a zip and uncompressing it in any deisred location):

``` bash
git clone https://github.com/nanoMLMS/pySNOW.git pysnow && cd pysnow
```

From here you can install the package by running:
```bash
pip install .
```

Automated tests can be run using pytest with the following command:
```bash
pytest .
```
from the `pySNOW` folder.

Requirments for `pySNOW` are [NumPy](https://numpy.org/) and [SciPy](https://scipy.org/), which are automatically installed with `pySNOW`. Additional optional dependencies is [tqdm](https://tqdm.github.io/) for progress bars to check progress of long computations
