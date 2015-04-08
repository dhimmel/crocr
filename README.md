## About CROCs

An unofficial *R* interface to the [*croc* python package](https://pypi.python.org/pypi/CROC/) providing tools for Condensed ROC (CROC) curves. CROCs transform the false positive rate (FPR, or x-axis of an ROC curve) to emphasize the performance of top predictions. Since the transformation applied to the FPR is continuous, this method has the advantage of upweighting *early retrieval* without relying on an arbitrary, binary threshold of where *early* ends. To learn more read the [publication](https://dx.doi.org/10.1093/bioinformatics/btq140) or browse the [python documentation](http://swami.wustl.edu/CROC/). 

Method publication:

> Swamidass SJ, Azencott CA, Daily K, Baldi P (2010). A CROC stronger than ROC: measuring, visualizing and optimizing early retrieval. *Bioinformatics*. [doi:10.1093/bioinformatics/btq140](https://dx.doi.org/10.1093/bioinformatics/btq140)

## About R interface

The interface works by making a system call from within *R*. Therefore the *croc* python package must be installed prior to use. The code has been designed for unix-like systems and may not work on other platforms. Currently only the exponential transformation is supported, although the code may provide a template for using a different transformation.

### Functions

#### Compute the CROC with an exponential FPR transform.
```R
CROC(score, status, directory, alpha=7)
```
where `score` is the predicted score/ranking, `status` is the binary outcome, `directory` (optional) specifies a directory to store temporary files and should not currently exist, and `alpha` is the exponential scaling parameter. Returns a list where `auc` is the area under the curve, `curve.df` is a data.frame of the CROC curve, and `random.df` is a data.frame of the CROC curve corresponding to a random classifier.

#### Find alpha from a predetermined FPR mapping.
```R
FindAlpha(fpr0, fpr1)
```
finds the value of *alpha* that maps `fpr0` to `fpr1` when performing the exponential transformation. This corresponds to the notation f(`fpr0`) = `fpr1` used by the paper. Currently, if the function returns an *alpha* greater than or equal to 750, the result is likely false. This occurs when mapping a very small FPR to a very large FPR and will not effect the range of scalings explored in the paper.

#### Exponentially transform a FPR.
```R
ExpTransform(fpr, alpha)
```
exponentially transforms a false positive rate (`fpr`). The transformation is scaled with `alpha`. 

