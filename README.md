## About CROCs

An unofficial *R* interface to the [*croc* python package](https://pypi.python.org/pypi/CROC/) providing tools for Condensed ROC (CROC) curves. CROCs transform the false positive rate (FPR, or x-axis of an ROC curve) to emphasize the performance of top predictions. Since the transformation applied to the FPR is continuous, this method has the advantage of upweighting *early retrieval* without relying on an arbitrary, binary threshold of where *early* ends. To learn more read the [publication](http://dx.doi.org/10.1093/bioinformatics/btq140) or browse the [python documentation](http://swami.wustl.edu/CROC/). 

Method publication:
> Swamidass SJ, Azencott CA, Daily K, Baldi P (2010). A CROC stronger than ROC: measuring, visualizing and optimizing early retrieval. *Bioinformatics* 26(10): 1348-1356

## About R interface

The interface works by making a system call from within *R*. Therefore the *croc* python package must be installed prior to use. Designed for unix-like systems. Currently only the exponential transformation is supported, although the code may provide a template for using a different transform.

### Functions

```R
CROC(score, status, directory, alpha=7)
```
where `score` is the predicted score/ranking, `status` is the binary outcome, `directory` (optional) specifies a directory to store temporary files and should not currently exist, and `alpha` is the exponential scaling parameter.

```R
FindAlpha(fpr0, fpr1)
```
returns the value of *alpha* that transforms an untransformed FPR (`fpr0`) to an exponentially scaled FPR (`fpr1`). Currently will not identify alphas exceeding 750.

```R
ExpTransform(fpr, alpha)
```
exponentially transforms a false positive rate (`fpr`). The transformation is scaled with `alpha`. 

