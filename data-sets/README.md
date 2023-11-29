# Creating data sets for U-Net training

## E906 messy MC

Follow the instructions in this [repository](https://github.com/abinashpun/seaquest-projects/tree/nmsu_ana/e906_gmc) to generate the E906 messy MC events.

## Apply basic cuts

We have applied basic cuts to improve the data quality. Cuts that are applied `mass > 5.` and `xF > 0.`. Change the cuts according to the analysis.

```
python SimpleTree.py
```

## Split for train, validation and test events

Here we split the events for training, cross validation and testing.

```
python SplitTree.py
```

## Make histograms with different $\lambda$, $\mu$ and $\nu$ combinations

```
mkdir build
cd build
root -b -e 'gSystem->CompileMacro("../MakeUNetData.cc", "kfgO", "make-unet-data");' -q

cd ..
root -b -e 'gSystem->Load("build/make-unet-data.so"); MakeUNetData(70000, 30000, 40000);'
```

## Save to tensor dataset

```
python SaveTensor.py
```