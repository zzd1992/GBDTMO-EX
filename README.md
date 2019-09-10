# GBDTMO-EX
This project provides examples for how to use [GBDT-MO](https://github.com/zzd1992/GBDTMO) and codes for reproduction the experiments in our preprint paper.

## How to use GBDT-MO
Suppose you have installed `gbdtmo`. If not, please refer [GBDT-MO](https://github.com/zzd1992/GBDTMO).

Find the path of `gbdtmo.so` and modify `Lib_path` in `cfg.py`.
```python
Lib_path = "path to gbdtmo.so"
```
Import `gbdtmo` and load the shared library file
```python
from gbdtmo import load_lib, GBDTSingle, GBDTMulti
import cfg

LIB = load_lib(cfg.Lib_path)
```
Build a `gbdtmo` instance, you must setup the output dimension.
```python
out_dim = 10
params = {"max_depth": 5, "lr": 0.1}
booster = GBDTMulti(LIB, out_dim=out_dim, params=params)
```
Setup your dataset, train and predict.
```python
booster.set_data((x_train, y_train), (x_valid, y_valid))
booster.train(num_rounds)
preds = booster.predict(x_valid)
```
Data in the first tuple is used for training. Data in the second tuple is used for validation which can be omitted. Items in tuples must be an numpy array.
Dump to text file or load from text file:
```python
booster.dump(path)
booster.load(path)
```
