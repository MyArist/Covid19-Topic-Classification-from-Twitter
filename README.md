# Topic Modelling for Covid-19

Here, I using LDA (Latent Dirichlet Allocation)

## Modules

There are quite a number of modules that I use

```
import os
import pandas as pd
import numpy as np
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
import plotly as py
import plotly.graph_objs as go
import gensim
from gensim import corpora, models, similarities
import logging
import tempfile
from nltk.corpus import stopwords
from string import punctuation
from collections import OrderedDict
import seaborn as sns
import pyLDAvis.gensim
import matplotlib.pyplot as plt
```

## Trend for May

Then I use **plotly module** for visualizing trend of tweets in May

```
tweets['datetime'] = pd.to_datetime(tweets['datetime'], format='%Y-%m-%d')
tweetsT = tweets['datetime']

trace = go.Histogram(
    x=tweetsT,
    marker=dict(
        color='blue'
    ),
    opacity=0.75
)

layout = go.Layout(
    title='Tweet Activity in May',
    height=450,
    width=1200,
    xaxis=dict(
        title='Date and Month'
    ),
    yaxis=dict(
        title='Tweet Quantity'
    ),
    bargap=0.2,
)

data = [trace]

fig = go.Figure(data=data, layout=layout)
py.offline.iplot(fig)
```

![Trend](https://github.com/MyArist/Topic-Modelling-for-Covid-19/blob/master/LDA/tren.png)

## Clustermap

I make clustermap to see the correlation each of word

```
g=sns.clustermap(df_lda.corr(), center=0, standard_scale=1, cmap="RdBu", metric='cosine', linewidths=.75, figsize=(15, 15))
plt.setp(g.ax_heatmap.yaxis.get_majorticklabels(), rotation=0)
plt.show()
```

![Clustermap](https://github.com/MyArist/Topic-Modelling-for-Covid-19/blob/master/LDA/clustermap.png)

## LDA

Finally, the LDA

![LDA](https://github.com/MyArist/Topic-Modelling-for-Covid-19/blob/master/LDA/lda.png)

There are two panels displayed by the pyLDAvis graph. The left panel shows a global view of the model, such as how common topics are and how topics relate to each other. The circle on the left panel shows the topic, the distance between circles shows the distance between topics, the prevalence of each topic is indicated by the circle area. Although topic prevalence can indicate which is the most dominant or important topic, prevalence has a disadvantage when comparing topics between topics because it is difficult to compare almost the same circle size. The distance of the circle also has the same weakness, which is difficult to measure the similarity of topics in a topic cluster. 

The right panel contains bar charts representing each word that is useful in interpreting the topic. The red diagram shows the frequency of words from related topics (red circle) and the blue diagram shows the wide frequency of the corpus. Above the bar chart is a tool to regulate relevance.
