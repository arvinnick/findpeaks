# findpeaks

[![Python](https://img.shields.io/pypi/pyversions/findpeaks)](https://img.shields.io/pypi/pyversions/findpeaks)
[![PyPI Version](https://img.shields.io/pypi/v/findpeaks)](https://pypi.org/project/findpeaks/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/erdogant/findpeaks/blob/master/LICENSE)
[![Github Forks](https://img.shields.io/github/forks/erdogant/findpeaks.svg)](https://github.com/erdogant/findpeaks/network)
[![GitHub Open Issues](https://img.shields.io/github/issues/erdogant/findpeaks.svg)](https://github.com/erdogant/findpeaks/issues)
[![Project Status](http://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active)
[![Downloads](https://pepy.tech/badge/findpeaks)](https://pepy.tech/project/findpeaks)
[![Downloads](https://pepy.tech/badge/findpeaks/month)](https://pepy.tech/project/findpeaks/month)
[![DOI](https://zenodo.org/badge/260400472.svg)](https://zenodo.org/badge/latestdoi/260400472)
[![Sphinx](https://img.shields.io/badge/Sphinx-Docs-Green)](https://erdogant.github.io/findpeaks/)
<!---[![BuyMeCoffee](https://img.shields.io/badge/buymea-coffee-yellow.svg)](https://www.buymeacoffee.com/erdogant)-->
<!---[![Coffee](https://img.shields.io/badge/coffee-black-grey.svg)](https://erdogant.github.io/donate/?currency=USD&amount=5)-->

The library ``findpeaks`` aims to detect peaks in a 1-dimensional vector and 2-dimensional arrays (images) without making any assumption on the peak shape or baseline noise. To make sure that peaks can be detected across global and local heights, and in noisy data, multiple pre-processing and denoising methods are implemented.

 
# 
**Star this repo if you like it! ⭐️**
#

#### Installation

Install findpeaks from PyPI (recommended).

```bash
pip install findpeaks
```

#### Import findpeaks package

```python
from findpeaks import findpeaks
```


### Documentation

I moved all examples to the [documentation pages](https://erdogant.github.io/findpeaks/).

* [Example 1: Find peaks in 1D-vector with low number of samples](https://erdogant.github.io/findpeaks/pages/html/Examples.html#d-vector)

<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig1_raw.png" width="400" />
</p>
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig1_interpol.png" width="400" />  
</p>

#### Example 2: 1D vector low resolution

```python
# Load library
from findpeaks import findpeaks
# Data
X = [10,11,9,23,21,11,45,20,11,12]
# Initialize
fp = findpeaks(method='peakdetect', lookahead=1)
results = fp.fit(X)
# Plot
fp.plot()

fp = findpeaks(method='topology', lookahead=1)
results = fp.fit(X)
fp.plot()
fp.plot_persistence()

```

<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig2_peakdetect.png" width="400" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig2_topology.png" width="400" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig2_persistence.png" width="400" />
</p>

```python
# Initialize with interpolate parameter
fp = findpeaks(method='peakdetect', lookahead=1, interpolate=10)
results = fp.fit(X)
fp.plot()

fp = findpeaks(method='topology', lookahead=1, interpolate=10)
results = fp.fit(X)
fp.plot()

```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig2_peakdetect_int.png" width="400" />  
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig2_topology_int.png" width="400" />  
  
</p>


#### Example 3: 1D-vector high resolution

```python
# Load library
import numpy as np
from findpeaks import findpeaks

# Data
i = 10000
xs = np.linspace(0,3.7*np.pi,i)
X = (0.3*np.sin(xs) + np.sin(1.3 * xs) + 0.9 * np.sin(4.2 * xs) + 0.06 * np.random.randn(i))

# Initialize
fp = findpeaks(method='peakdetect')
results = fp.fit(X)
# Plot
fp.plot1d()

fp = findpeaks(method='topology', limit=1)
results = fp.fit(X)
fp.plot1d()
fp.plot_persistence()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig3.png" width="600" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig3_topology.png" width="600" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig3_persistence_limit.png" width="600" />
</p>


#### Example 4: 2D-array (image) using default settings

```python
# Import library
from findpeaks import findpeaks

# Import example
X = fp.import_example()
print(X)
array([[0. , 0. , 0. , 0. , 0. , 0. , 0. , 0. , 0.4, 0.4],
       [0. , 0. , 0. , 0. , 0. , 0. , 0.7, 1.4, 2.2, 1.8],
       [0. , 0. , 0. , 0. , 0. , 1.1, 4. , 6.5, 4.3, 1.8],
       [0. , 0. , 0. , 0. , 0. , 1.4, 6.1, 7.2, 3.2, 0.7],
       [..., ..., ..., ..., ..., ..., ..., ..., ..., ...],
       [0. , 0.4, 2.9, 7.9, 5.4, 1.4, 0.7, 0.4, 1.1, 1.8],
       [0. , 0. , 1.8, 5.4, 3.2, 1.8, 4.3, 3.6, 2.9, 6.1],
       [0. , 0. , 0.4, 0.7, 0.7, 2.5, 9. , 7.9, 3.6, 7.9],
       [0. , 0. , 0. , 0. , 0. , 1.1, 4.7, 4. , 1.4, 2.9],
       [0. , 0. , 0. , 0. , 0. , 0.4, 0.7, 0.7, 0.4, 0.4]])

# Initialize
fp = findpeaks(method='mask')
# Fit
fp.fit(X)

# Plot the pre-processing steps
fp.plot_preprocessing()
# Plot all
fp.plot()

# Initialize
fp = findpeaks(method='topology')
# Fit
fp.fit(X)

```

The input figure
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/plot_example.png" width="100" />
</p>

The masking approach detects the correct peaks.
```python
fp.plot()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_mask.png" width="600" />
</p>

Conversion from 2d to 3d mesh plots looks very nice. But there is a rough surface because of the low-resolution input data.
```python
fp.plot_mesh()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_mesh1.png" width="600" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_mesh2.png" width="600" />
</p>

The persistence plot appears to detect the right peaks.
```python
fp.plot_persistence()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_pers.png" width="600" />
</p>


#### Example 5: 2D-array (image) with pre-processing steps

```python
# Import library
from findpeaks import findpeaks

# Import example
X = fp.import_example()

# Initialize
fp = findpeaks(method='topology', scale=True, denoise=10, togray=True, imsize=(50,100), verbose=3)

# Fit
results = fp.fit(X)

# Plot all
fp.plot()

```

Show the plots:

```python
fp.plot_preprocessing()
```

<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_raw.png" width="100" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_interpolate.png" width="100" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_raw_processed.png" width="100" />
</p>

The masking does not work so well because the pre-processing steps includes some weighted smoothing which is not ideal for the masking approach.
```python
fp.plot()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_mask_proc.png" width="600" />
</p>

The mesh plot has higher resolution because the pre-processing steps caused some smoothing.
```python
fp.plot_mesh()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_meshs1.png" width="600" />
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_meshs2.png" width="600" />
</p>

The Persistence plot does show the detection of correct peaks.
```python
fp.plot_persistence()
```
<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/2dpeaks_perss.png" width="600" />
</p>


Denoising example
```python
from findpeaks import findpeaks
fp = findpeaks()
img = fp.import_example('2dpeaks_image')
import findpeaks

# filters parameters
# window size
winsize = 15
# damping factor for frost
k_value1 = 2.0
# damping factor for lee enhanced
k_value2 = 1.0
# coefficient of variation of noise
cu_value = 0.25
# coefficient of variation for lee enhanced of noise
cu_lee_enhanced = 0.523
# max coefficient of variation for lee enhanced
cmax_value = 1.73

# Some pre-processing
# Resize
img = findpeaks.stats.resize(img, size=(300,300))
# Make grey image
img = findpeaks.stats.togray(img)
# Scale between [0-255]
img = findpeaks.stats.scale(img)

# Denoising
# fastnl
img_fastnl = findpeaks.stats.denoise(img.copy(), method='fastnl', window=winsize)
# bilateral
img_bilateral = findpeaks.stats.denoise(img.copy(), method='bilateral', window=winsize)
# frost filter
image_frost = findpeaks.frost_filter(img.copy(), damping_factor=k_value1, win_size=winsize)
# kuan filter
image_kuan = findpeaks.kuan_filter(img.copy(), win_size=winsize, cu=cu_value)
# lee filter
image_lee = findpeaks.lee_filter(img.copy(), win_size=winsize, cu=cu_value)
# lee enhanced filter
image_lee_enhanced = findpeaks.lee_enhanced_filter(img.copy(), win_size=winsize, k=k_value2, cu=cu_lee_enhanced, cmax=cmax_value)
# mean filter
image_mean = findpeaks.mean_filter(img.copy(), win_size=winsize)
# median filter
image_median = findpeaks.median_filter(img.copy(), win_size=winsize)

```

Plotting

```python
import matplotlib.pyplot as plt
plt.figure(); plt.imshow(img_fastnl, cmap='gray'); plt.title('Fastnl'); plt.grid(False)
plt.figure(); plt.imshow(img_bilateral, cmap='gray'); plt.title('Bilateral')
plt.figure(); plt.imshow(image_frost, cmap='gray'); plt.title('Frost')
plt.figure(); plt.imshow(image_kuan, cmap='gray'); plt.title('Kuan')
plt.figure(); plt.imshow(image_lee, cmap='gray'); plt.title('Lee')
plt.figure(); plt.imshow(image_lee_enhanced, cmap='gray'); plt.title('Lee Enhanced')
plt.figure(); plt.imshow(image_mean, cmap='gray'); plt.title('Mean')
plt.figure(); plt.imshow(image_median, cmap='gray'); plt.title('Median')
```

Find peaks on the denoised image
```python
from findpeaks import findpeaks
fp = findpeaks(scale=False, denoise=None, togray=False, imsize=False, verbose=3)
fp.fit(image_lee_enhanced)
fp.plot_persistence()
fp.plot_mesh(wireframe=False, title='image_lee_enhanced')
```


#### Find peaks and valleys in stock market data

```python
# Import library
from findpeaks import findpeaks
# Initialize findpeaks with cearus method.
# The default setting is that it only return peaks-vallyes with at least 5% difference. We can change this using params
fp = findpeaks(method='caerus')
# Import example data
X = fp.import_example('facebook')
# Fit
results = fp.fit(X)
# Make the plot
fp.plot()
```

<p align="center">
  <img src="https://github.com/erdogant/findpeaks/blob/master/docs/figs/fig_facebook_minperc5.png" width="600" />
</p>

### Citation
Please cite in your publications if this is useful for your research (see citation).

### Maintainer
	* Erdogan Taskesen, github: [erdogant](https://github.com/erdogant)
	* Contributions are welcome.
	* If you wish to buy me a <a href="https://www.buymeacoffee.com/erdogant">Coffee</a> for this work, it is very appreciated :)
	* See [LICENSE](LICENSE) for details.

#### References
* https://github.com/erdogant/findpeaks
* https://github.com/Anaxilaus/peakdetect
* https://www.sthu.org/blog/13-perstopology-peakdetection/index.html

