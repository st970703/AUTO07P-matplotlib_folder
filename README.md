# AUTO07P-matplotlib_folder<br />

There was an error when plotting with auto07p.<br />
The error appeared when trying to zoom in the graph.<br />
The graph would remain unchanged and unable to be zoomed in.<br />

### deatils of the inder error:<br />
```
File "/usr/lib/python3/dist-packages/matplotlib/ticker.py", line 1761, in _raw_ticks<br />
    istep = np.nonzero(steps >= raw_step)[0][0]<br />
IndexError: invalid index to scalar variable.<br />
```

### Solution to the indexError:<br />
Firstly, access ticker.py by using the following command:<br />
```
cd /usr/local/lib/python2.7/dist-packages/matplotlib<br />
```
Or a command similar, depending on your matplotlib location.<br />

Open the python file and replace the line in ticker.py:<br />
```
istep = np.nonzero(steps >= raw_step)[0][0]<br />
```

The line should be at line 1761, in _raw_ticks.<br />

Replace that line with the following:<br />
```
arr_dim = np.nonzero(steps >= raw_step).ndim<br />
if arr_dim == 1:<br />
  istep = np.nonzero(steps >= raw_step)[0]<br />
elif arr_dim == 2:<br />
  istep = np.nonzero(steps >= raw_step)[0][0]<br />
```
  
This should solve the error. It checks the dimension of the array before selecting the first element.<br />
