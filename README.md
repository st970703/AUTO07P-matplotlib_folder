# AUTO07P-matplotlib_folder

There was an error when plotting with auto07p.
The error appeared when trying to zoom in the graph.
The graph would remain unchanged and unable to be zoomed in.

deatils of the inder error:
File "/usr/lib/python3/dist-packages/matplotlib/ticker.py", line 1761, in _raw_ticks
    istep = np.nonzero(steps >= raw_step)[0][0]
IndexError: invalid index to scalar variable.

Solution to the indexError:
Just replace the line in ticker.py:
istep = np.nonzero(steps >= raw_step)[0][0]

Replace that line with the following:
arr_dim = np.nonzero(steps >= raw_step).ndim
if arr_dim == 1:
  istep = np.nonzero(steps >= raw_step)[0]
elif arr_dim == 2:
  istep = np.nonzero(steps >= raw_step)[0][0]
  
This should solve the error. It checks the dimension of the array before selecting the first element.
