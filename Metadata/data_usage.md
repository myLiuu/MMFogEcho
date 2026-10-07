# Data usage

Each scene's `annotations.json` links echoes to their temporally paired images through the `echo` and `image` paths.

For echo-to-image associations, use `reference_depth_m`, the reference target range obtained under fog-free conditions, as $r$. Let $\theta$ and $\phi$ denote the angles stored in `angle.azimuth_deg` and `angle.elevation_deg` in `annotations.json`, respectively, converted from degrees to radians. The corresponding LiDAR point is:

$$
\mathbf{p}_L =
\begin{bmatrix}
r\cos\phi\cos\theta\\
r\cos\phi\sin\theta\\
r\sin\phi
\end{bmatrix}.
$$

Transform the point into camera coordinates:

$$
\mathbf{p}_C = R\mathbf{p}_L + \mathbf{t}
= \begin{bmatrix}X_C&Y_C&Z_C\end{bmatrix}^{T}.
$$

The corresponding pixel coordinates are:

$$
u = f_x\frac{X_C}{Z_C}+c_x,
\qquad
v = f_y\frac{Y_C}{Z_C}+c_y.
$$

Here, $R$, $\mathbf{t}$, $f_x$, $f_y$, $c_x$, and $c_y$ are supplied in `Calibration/camera_lidar.json`, together with the coordinate conventions.

A 25 × 25 image patch centered at $(u, v)$ is then extracted from the paired image.

For point cloud generation, decode waveforms using `Metadata/data_format.json` and estimate return ranges following Eq. (9) in the associated paper, with time delays measured relative to `reference_index`. Convert these ranges to LiDAR points using the annotated scanning angles and the coordinate conversion above.