# Sentinel 2 Data Fetcher
This Python library simplifies the download of satellite images from the Copernicus Sentinel-2 satellite.
The data are fetched from the Google cloud storage [Sentinel-2 data](https://cloud.google.com/storage/docs/public-datasets/sentinel-2).
Please feel free to contact us if you find issues or have any suggestions for improvements. See for an example tests/main.py.

<a href="https://pypi.python.org/pypi/sat-mapping-cyborg-ai" rel="nofollow">
<img alt="pypi" src="https://img.shields.io/badge/pypi-0.0.37-success">
</a>

## Installation

- Create a Virtual Environment and activate it.
    
    ```shell
    python3 -m venv venv
    . venv/bin/activate
    ```

- Install the Package via pip.

    ```shell
    pip install sat-mapping-cyborg-ai
    ```
  
## Usage

- Import the Library

    ```python
    from sat_mapping import FolderData, folders_time_frame, Paths, download
    ```
  
- Set the Path to where you want to store the Satellite Data.

    ```python
    paths = Paths("<ANY/VALID/PATH>")
  
    ```

- Start the Download. (Note: One year needs around 110 GB Disk Space.)
  - The download uses Google gsutil if there is no gsutil configuration (.boto) in your home directory, gsutil config will be called to generate one.  
  - Gsutil config asks the user for a token and a Google project id. 
  - For tiles see [Sentinel-2 data](https://cloud.google.com/storage/docs/public-datasets/sentinel-2).

    ```python 
    download(paths, years=[2019], tiles=["32TMT"], months=[7, 11])
    ```
  
- Load a folder.

    ```python
    folder_name = paths.folders[0]
    upper_left = (100000.0, 0.0)       # Postion on tile in [m]
    lower_right = (109800.0, 10000.0)  # Postion on tile in [m]
    data = FolderData(join(paths.data_path, folder_name), upper_left, lower_right)
    ```
  
- Display the image. (if matplotlib is not installed use <code>pip install matplotlib</code>)

    ```python
    import matplotlib.pyplot as plt
  
    picture = data.data[:, :, [3, 1, 2]]  # NIR, GREEN, BLUE
    fig: plt.Figure = plt.figure()
    plt.imshow(picture)
    plt.show()
    ```
