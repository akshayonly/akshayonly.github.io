---
layout: article
title:  "Visualizing MeSH terms as a Network Graph"
tags: MeSH PubMed E-utilities Biopython Pyvis
mode: immersive
aside:
  toc: false
header:
  theme: dark
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: assets/post-imgs/p1-header-01.png
---
In this article, we would visualize MeSH terms associated with any PubMed article as a Network-graph.<!--more--> 

# Introduction
<center>
  <div class="card card--flat">
    <div class="card__content">
      <p>"When you visualize, then you materialize." </p>
      <p><cite>&mdash; Denis Waitley</cite></p>
    </div>
  </div>
</center>

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas tincidunt ornare nibh, non elementum augue tempus eget. Pellentesque tempus scelerisque iaculis. Nullam interdum ultricies nibh quis sollicitudin. Donec ornare fermentum facilisis. Ut at sem ac sem imperdiet varius a eget tortor. Nam eu augue eget orci semper maximus in eget augue. Mauris ornare, nisl ut suscipit consectetur, mi quam interdum tellus, at rutrum quam eros ultrices mi.

```mermaid
graph TB;
    A[PMID]
    B[Entrez.efetch( )]
    C[Medline.parse( )]
    D[record]
    E[Mesh Terms]
    F[pyvis.network]
    A-->B;
    B-->C;
    C-->D;
    D-->E;
    E-->F;    
```

# Handling millions of biomedical citations

PubMed is a search engine-like resource that provides access to biomedical and life sciences literature. In another word, it’d a freely available database that stores more than 33 million citations and abstracts of biomedical literature. Now searching through millions of records and retrieval of specific literature based on user-given queries or topics can be challenging. If the query is about ‘Cancer’, you don’t want to return information related to some other disease like ‘Malaria’. Also, terms such as ‘Neoplasm’, ‘Tumour’ and ‘Cancer’ are umbrella terms, so in order to deal with such and more issues, the Medical Subject Headings (MeSH) were introduced. 

# Primer on Graph theory with pyvis

The standard Lorem Ipsum passage, used since the 1500s “Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.”

{% highlight python linenos %}
from pyvis.network import Network
G = Network()
{% endhighlight %}

# Visualizing MeSH terms

The standard Lorem Ipsum passage, used since the 1500s “Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 

~~~ python
from pyvis.network import Network
G = Network()
~~~

Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.”

