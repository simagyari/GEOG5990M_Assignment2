# Industrial Site Locator

Author: [simagyari](https://github.com/simagyari)  
Version: 1.0.0

## Description
This software was made as an assignment piece for **GEOG5990M Programming for Geographical Information Analysis: Core Skills**. The software implements a GUI-based industrial site locator, taking in three basemaps (geology, population, transport), then weighting and averaging them to produce a final representation, based on the user-defined importance of each of the three factors. The application enables the user to display the top 10% of the suitability scale in a blue colormap, as opposed to the default grayscale. Moreover, the user can save the final weighted map as a .csv file to any location on the computer via the in-built file explorer. More on the usage in [What to expect while running the code](#what-to-expect-while-running-the-code).

## Software requirements
The code was run on a [Windows](https://www.microsoft.com/en-us/windows?r=1) 11 operating system, while [Python](https://www.python.org/) and [Jupyter](https://jupyter.org/) was operated through the [Anaconda](https://www.anaconda.com/) distribution. The versions of Python and the packages, except for those needed for the Jupyter capabilities to run, are displayed below:

| **Software** | **Version** |
| :------- | :-----: |
| Python (packages below) | 3.9.7 |
| - matplotlib | 3.4.3 |
| - csv | 1.0 |
| - tk | 8.6.11 |
| - numpy | 1.20.3 |

## Installation
To install the model, you will need to download or clone the source code from the [project repository](https://github.com/simagyari/GEOG5990M_Assignment2). If you are only interested in running the application, you can download only the `src` folder's contents. The necessary files for the model to run are:
- sitelocation.ipynb
- geology.csv
- population.csv
- transport.csv

The code can be installed to your preferred folder; however, it is advised to choose it so that you do not interfere with other applications.

Once installed, the software is ready to be used, provided that the [software requirements](#software-requirements) are satistifed.

## Contents of the software

| **File** | **Description** |
| :--- | :---------- |
| src/sitelocation.ipynb | Contains the code for the locator to run. |
| src/geology.csv | Contains the geology basemap. |
| src/population.csv | Contains the population basemap. |
| src/transport.csv | Contains the transport basemap. |
| tests/test_sitelocation.ipynb | Contains unittest functions to test the sitelocation methods. |
| tests/test_raster.csv | Contains a simple (3-by-3) test raster. |
| tests/test_raster_2.csv | Contains another simple (3-by-3) test raster |
| README.md | Contains the instructions and important information about the software. |
| .gitignore | Specifies files that should be ignored by the local git installation. |
| LICENSE | Contains licensing information of the software. |

## Running the application
The model can be run from the Command Prompt or Powershell on Windows, Terminal on MacOS and Linux distibutions. The code to initialise the model is the following:
```
jupyter nbconvert --inplace --to notebook --execute --allow-errors sitelocation.ipynb
```
The `--inplace` keyword overwrites the notebook every time it gets executed, creating a new file. Since there are no outputs generated in the notebook, the resulting file will be the same as the one being run.

Alternatively, the software can be run from the Jupyter Notebook interface. It can be initialised from the Terminal or Command Prompt/Powershell from the folder of the notebook by typing `jupyter notebook`. This will open a browser window with the notebook directory in it. Opening the notebook file, it can be run from the toolbar or each cell can be run by itself. Once the imports and the class definition has been run, it is enough to repeatedly run the last cell for multiple usage of the application.

### What to expect while running the code
Once running the above script from the CMD/Powershell/Terminal, a [Tkinter](https://docs.python.org/3/library/tkinter.html) window will open containing the software GUI. On the left side, the three scalebars can be used to set the importance of each input layer (geology, population, transport). All scalebars are initialised with the value of 100, meaning 100% importance. Below the scalebars, a checkbox toggles the blue representation of the top 10% of map values. It is initialised inactively. Below the checkbox, on the left, the `Display map` button initiates the plotting of the map with the currently set weights. On the right, the `Save map` button opens a file dialog window to specify the place and name of the current map to save.

The right side of the application window starts out empty, upon clicking the `Display map` button, the weighted map will be plotted there.

**IMPORTANT: toggling the blue representation instantly plots the currently set weights for the map, there is no need to push `Display map` again.**

Once you have finished the work and possibly saved your desired maps, you can exit the application by clicking on the red cross sign in the top right corner.

## Testing
Testing of the agentframework methods were conducted using the [unittest](https://docs.python.org/3/library/unittest.html) library of Python. The library facilitates testing different units of the code independently. In this case, tested functions were tested to give the appropriate results when fed with appropriate parameters. The test file is included in the repository, names "tests_sitelocation.ipynb". It contains the full code with informative comments on the testing and the exact processes undertaken.

## Profiling
For profiling, the code has been converted to a Python file (.py). This enabled the file-wide usage of the appropriate testing packages, while not affecting the performance of the code much. Thus, the results remain representative to the notebook file published.

The computer used for profiling had the following specifications:

| **Hardware** | **Specification** |
| :------- | :------------ |
| Processor | AMD Ryzen 7 4800H 2.90 GHz |
| RAM | 32 GB |
| OS | Windows 11 Pro x64 version 21H2 |

The code has been profiled for speed using [cProfile](https://docs.python.org/3/library/profile.html). During a run of approximately 70 seconds, with multiple triggers of each method, none of them yielded a per call time above 0.2 seconds, except for those that require human interaction, such as the save() method.

Memory profiling was carried out using [memory-profiler](https://pypi.org/project/memory-profiler/). Multiple runs showed that a consistent memory usage between 90 and of 130 MiB can be observed, with the latter only reached during saving maps.

## Known issues
Since the application does not require user-specified arguments, and everything is controlled by checkboxes and scalebars, it is harder to induce an error or issue for the GUI user.

There are no major issues known with the code when run from the CMD/Powershell/Terminal.

When run from the Jupyter Notebook interface, if the imports cell is run more than once without restarting the kernel inbetween, an error is thrown due to the matplotlib backend usage, which collides with the Qt specification for non-inline plotting. This error can be avoided by only running the imports cell once per session, or, if re-running is unavoidable, restarting the kernel between two runs.

## Future development ideas

In the future, there are some options to enhance the code.

1. For placing the widgets in the GUI, the place() package manager of tkinter was used, which makes updates hard, as it requires overwriting positions one-by-one. This can be replaced by the grid() package manager, which provides more flexible update setups.
2. Menu options can be created for the application that enable users to specify their own input maps from different locations on the computer, or even online. The number of input maps can be made customisable.
3. Interactive plotting of the weighted map can be implemented for easier comparison of exact places on the map.
4. Zooming capability with automatically adjusting color scheme can be implemented to let users focus on particular sites.
5. Vector maps can be overlayed with the suitability representation to provide easier access to site information and availability.

#### Thank you for reading through this README file, I hope you will find this program useful.
