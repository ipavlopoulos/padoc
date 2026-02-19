# Dating Greek Papyri with Text Regression
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

Dating Greek papyri accurately is crucial not only to edit their texts but also to understand numerous other aspects of ancient writing, document and book production and circulation, as well as various other aspects of administration, everyday life and intellectual history of antiquity. Although a substantial number of Greek papyri documents bear a date or other conclusive data as to their chronological placement, an even larger number can only be dated tentatively or in approximation, due to the lack of decisive evidence. 

We created a dataset of 389 transcriptions of documentary Greek papyri, dated from the 3rd century BCE to the 7th century CE, originating mainly from Greco-Roman Egypt. You may find this dataset in this repository (`data/padoc/padoc389.csv`). We used this dataset to train 389 regression models, showing an average mean absolute error of 54 years (MSE of 1.17) when predicting the date of these papyri, outperforming the baseline and image classifiers. Using an ensemble of these regressors, then, [we computed and release date estimations](https://github.com/ipavlopoulos/padoc/blob/main/data/in_the_wild.csv) for 159 manuscripts (in blue, in the figure below), for which only the upper limit (in red) is known. 

<img width="1990" height="290" alt="image" src="https://github.com/user-attachments/assets/f3ee83bd-fde4-4fe2-b007-828561660bb4" />

Some of our estimations fall far away from the (red) upper limit while others fall close. The estimated date should be read along with other information (in the shared corpus), such as the place settlement. We observe, for example, that in some places the estimated dates fall closer to the upper limit (e.g., in Oxyrhynchos and Tebtynis the distance is 132 years) compared to others (e.g., in Antinoopolis and Hermopolis the distance is 283 and 384 years). See Section 7.2 of the paper for more details.

To access the data, you can download the repository and run the following code in Python (also in a notebook in the repo):

```python
import pandas as pd
wild = pd.read_csv('data/in_the_wild.csv')
norm = lambda x: x if str(x)=="4" else int(str(x)[:5]) if str(x).startswith("-") else int(str(x)[:4])
wild["by"] = wild.Date_notAfter.apply(norm)
wild = wild.sort_values(by="by", ascending=False)
wild.sample()
```

The study was presented as a long article at ACL 2023 in Toronto, Canada. You may access it online [https://aclanthology.org/2023.acl-long.556](https://aclanthology.org/2023.acl-long.556) or watch [the recorded presentation](https://aclanthology.org/2023.acl-long.556.mp4). 

If you find this study useful, please use the following information to cite:

```
@inproceedings{pavlopoulos-etal-2023-dating,
    title = "Dating {G}reek Papyri with Text Regression",
    author = "Pavlopoulos, John  and
      Konstantinidou, Maria  and
      Marthot-Santaniello, Isabelle  and
      Essler, Holger  and
      Paparigopoulou, Asimina",
    editor = "Rogers, Anna  and
      Boyd-Graber, Jordan  and
      Okazaki, Naoaki",
    booktitle = "Proceedings of the 61st Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)",
    month = jul,
    year = "2023",
    address = "Toronto, Canada",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.acl-long.556/",
    doi = "10.18653/v1/2023.acl-long.556",
    pages = "10001--10013",
}
```
