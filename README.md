# AUTO07P-matplotlib_folder<br />

There was an error when plotting with auto07p.<br />
The error appeared when trying to zoom in the graph.<br />
The graph would remain unchanged and unable to be zoomed in.<br />

### deatils of the index error:<br />
```
File "/usr/lib/python3/dist-packages/matplotlib/ticker.py", line 1761, in _raw_ticks
    istep = np.nonzero(steps >= raw_step)[0][0]
IndexError: invalid index to scalar variable.
```

### Solution to the indexError:<br />
Firstly, access ticker.py by using the following command:<br />
```
cd /usr/local/lib/python2.7/dist-packages/matplotlib
```
Or a command similar, depending on your matplotlib location.<br />

Open the python file and replace the line in ticker.py:<br />
```
istep = np.nonzero(steps >= raw_step)[0][0]
```

The line should be at line 1761, in _raw_ticks.<br />

Replace that line with the following:<br />
```
arr_dim = np.nonzero(steps >= raw_step).ndim
if arr_dim == 1:
  istep = np.nonzero(steps >= raw_step)[0]
elif arr_dim == 2:
  istep = np.nonzero(steps >= raw_step)[0][0]
```
  
This should solve the error. It checks the dimension of the array before selecting the first element.<br />
