# Digital signal processing portfolio

Six signal processing projects in Python, each taking a real measured signal
and doing something useful with it. From EERI414, Digital Signal Processing, in
my Computer and Electronic Engineering degree at North-West University.

NumPy, SciPy, statsmodels, matplotlib. Each project is a notebook with the
working written out, because in every one the interesting part was choosing the
method and justifying the parameters, not calling the library function.

## Projects

### `01-ecg-iir-filters/` — Alertness monitoring from ECG

Separating heart rate variability into its frequency bands to detect falling
alertness, which matters in jobs where a lapse in attention is dangerous.

IIR bandpass filters designed for the LF and HF bands of the HRV spectrum. The
design work is in the bilinear transform and the frequency pre-warping it
needs: warp the specification before designing in the analogue domain, or the
digital filter's band edges land in the wrong place.

Done with a project partner. I did the design procedure and the HF band; the
partner did the LF band demonstration. The notebook marks which sections are
whose.

### `02-thd-fir-filter-bank/` — Total harmonic distortion of a motor current

Measuring THD on a blocked-rotor current waveform from an induction motor,
using a bank of FIR filters to pull out each harmonic rather than reading them
off an FFT.

The point of the filter bank over the FFT is leakage. If the fundamental is not
exactly an integer number of bins, its energy smears across the spectrum and
contaminates the harmonic estimates. A filter bank tuned to each harmonic
avoids the problem at the cost of designing and validating every filter.

### `03-eigenfaces-pca/` — Facial recognition with PCA

The classic eigenfaces method: treat each face image as a very long vector,
mean-centre the set, find the principal components of the covariance, and
project faces into the low-dimensional space those components span.

The practical trick in here is the covariance step. The covariance matrix of
raw image vectors is far too large to decompose directly, so the eigenvectors
are computed from the much smaller matrix formed the other way round and mapped
back.

### `04-kalman-position/` — Position estimation from phone accelerometer data

Estimating the position of a phone being carried, from its accelerometer alone.

Integrating acceleration twice turns a small bias into a position error that
grows with the square of time, so raw integration is useless within seconds. A
Kalman filter with a constant-velocity model keeps the estimate bounded by
weighting the prediction against the noisy measurement. Includes the
preprocessing: resampling to a uniform rate and Butterworth filtering before
the filter sees anything.

### `05-stl-arima-forecasting/` — Platinum price forecasting

Forecasting platinum closing prices with STL decomposition and ARIMA.

STL splits the series into trend, seasonal and remainder so each can be handled
appropriately. The series has an obvious change in behaviour partway through,
which is the honest difficulty in the notebook: a model fitted across a
structural break forecasts the past rather than the future, so part of the work
is deciding what to fit on.

### `06-temperature-forecasting/` — Minimum temperature forecasting

The module's examination project, done individually over a week and defended in
an oral examination. Daily minimum air temperatures from four South African
weather stations, with the goal of forecasting Potchefstroom.

The brief asked for two fundamentally different analyses of the signal, four
fundamentally different filtering techniques and two fundamentally different
prediction algorithms, each choice motivated and compared on measured results.
The notebook works through time-domain statistics and frequency-domain
analysis, then Wiener and Kalman filtering alongside the classical approaches,
and finishes with STL decomposition and ARIMA forecasts.

Filters are built from their design procedure rather than called as one-line
library functions, which is why the notebook is long.

## The data

Input data is not included. The ECG recordings, motor current measurements,
face image set, accelerometer log and price series were supplied with the
course and are not mine to redistribute. Each notebook states the file it
expects in a `data/` directory alongside it.

## Running

```
pip install numpy scipy statsmodels matplotlib pandas scikit-learn
```

Notebooks are committed with outputs cleared, so they read as code rather than
as a wall of plots. Run them to regenerate the figures.

## Licence

MIT, see `LICENSE`, covering my code. It does not cover the datasets.
