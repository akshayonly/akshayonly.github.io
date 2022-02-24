---
layout: article
title:  "Visualizing Scientific Articles as a Network Graph"
tags: MeSH PubMed E-utilities Biopython Pyvis
aside:
  toc: false
mode: immersive
header:
  theme: dark
article_header:
  type: cover
  image:
    src: assets/Post-01-Imgs/1.png
---
In Development.
{:.warning}

In this article, we would visualize MeSH terms associated with any PubMed article as a Network-graph.<!--more--> 

CONTENT

1. Introduction
2. PubMed, Medline & Entrez
3. Medical subject headings (MeSH)
4. Biological Named-entity recognition (BioNER)
5. Building & Visualising Graphs with Networkx & Pyvis
6. Abstract as Network Graph
7. MeSH terms as Network Graph
8. Conclusion
9. Summary
10. References

# Introduction
<center>
  <div class="card card--flat">
    <div class="card__content">
      <p>"When you visualize, then you materialize." </p>
      <p><cite>&mdash; Denis Waitley</cite></p>
    </div>
  </div>
</center>

A while back, I came across Obsidian which is a Note-taking application. One of its key features is creating connections between different notes. It lets users view these inter-connections in a - Graph view which is pretty amazing! Check out the below screenshots.

![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/2.png "Image_shadow"){:.rounded}
<br>
<br>
![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/3.png "Image_shadow"){:.rounded}


Forming such a network connection helps us understand relationships between entities. Apart from visualizing interconnected notes, such network-graph or graphs have actual scientific use cases. The image below displays the protein interactome-based study of schizophrenia, and another image displays the network analysis and visualization of political blogs preceding the U.S. Presidential Election of 2004.

![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/4.png "Image_shadow"){:.rounded}
<br>
<br>
![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/5.png "Image_shadow"){:.rounded}

This let me ponder upon different possibilities. I thought, wouldn’t it would be great if we can represent a scientific article (or biomedical literature) in a graph manner? But why should anyone visualize scientific literature as a network graph? Simple answer, for getting a high-level overview of relevant terms before jumping into reading the article.

But how can we do this? I started researching (googling) whether such tools or platforms exist. I came across connected papers, this site builds graphs of related papers based on the user-given paper. Cool visualization, but not what we want. So let's build our own tool but this isn’t straightforward also, there are a few issues here:

1. Not all biomedical articles or literature is accessible. i.e., paywalls.
2. Even if we get articles that are accessible, processing on average 6-9 pages of PDFs can be a little tricky.
3. Also, if we scale up to incorporate many articles this can prove challenging. Because there can be different words with similar meanings. 

So to tackle the above issues and to keep hands simple we'd use MeSH terms which are present for most of the biomedical literature & also apply an NLP technique known as Entity-named recognition to extract key terms. (We'd learn more about them below)

# PubMed, Medline & Entrez
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Cras adipiscing enim eu turpis egestas pretium. Cursus turpis massa tincidunt dui. Vulputate ut pharetra sit amet aliquam. Eleifend mi in nulla posuere sollicitudin aliquam ultrices sagittis orci. Varius morbi enim nunc faucibus. Urna molestie at elementum eu facilisis sed odio. Amet consectetur adipiscing elit ut. Porttitor rhoncus dolor purus non. Congue nisi vitae suscipit tellus mauris a diam maecenas.

Turpis in eu mi bibendum. Lobortis elementum nibh tellus molestie nunc non blandit massa enim. Viverra ipsum nunc aliquet bibendum enim. Vulputate sapien nec sagittis aliquam malesuada bibendum arcu. Convallis posuere morbi leo urna molestie at elementum. Arcu cursus vitae congue mauris rhoncus. Nisl nunc mi ipsum faucibus vitae aliquet. Magna fermentum iaculis eu non diam phasellus vestibulum lorem sed. Leo vel fringilla est ullamcorper eget nulla. Semper quis lectus nulla at volutpat diam.

~~~ bash
!pip install -q biopython
~~~
Once it gets install, let's import the modules
~~~ python
from Bio import Entrez
from Bio import Medline
~~~
Below function utilises efetch function of Entrez to return MEDLINE record for given PMID of PubMed article.

~~~ python
def fetch_data(pmids):
    """Returns MEDLINE record associated with the PMID(s)"""
    
    Entrez.email = 'akishirsath@gmail.com'

    # Extracting MEDLINE record for the given PMID(s)
    handle = Entrez.efetch(db="pubmed", 
                           id=pmids, 
                           rettype="medline", 
                           retmode="text")

    # Parsing the XML format 
    records = Medline.parse(handle)    
    
    return list(records)
~~~

# Medical subject headings (MeSH)

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Cras adipiscing enim eu turpis egestas pretium. Cursus turpis massa tincidunt dui. Vulputate ut pharetra sit amet aliquam. Eleifend mi in nulla posuere sollicitudin aliquam ultrices sagittis orci. Varius morbi enim nunc faucibus. Urna molestie at elementum eu facilisis sed odio. Amet consectetur adipiscing elit ut. Porttitor rhoncus dolor purus non. Congue nisi vitae suscipit tellus mauris a diam maecenas.

Turpis in eu mi bibendum. Lobortis elementum nibh tellus molestie nunc non blandit massa enim. Viverra ipsum nunc aliquet bibendum enim. Vulputate sapien nec sagittis aliquam malesuada bibendum arcu. Convallis posuere morbi leo urna molestie at elementum. Arcu cursus vitae congue mauris rhoncus. Nisl nunc mi ipsum faucibus vitae aliquet. Magna fermentum iaculis eu non diam phasellus vestibulum lorem sed. Leo vel fringilla est ullamcorper eget nulla. Semper quis lectus nulla at volutpat diam.

~~~ python
data_dict.get('MH', 'NONE')
~~~
OUTPUT
~~~
['*Alzheimer Disease/diagnosis/epidemiology/physiopathology', 'Humans']
~~~

# Biological Named-entity recognition (BioNER)
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget sit amet tellus cras adipiscing enim eu turpis. Sagittis orci a scelerisque purus semper. Tempor id eu nisl nunc mi ipsum faucibus vitae. At elementum eu facilisis sed odio morbi quis commodo odio. Eget lorem dolor sed viverra. In dictum non consectetur a erat nam at lectus urna. Imperdiet proin fermentum leo vel orci porta. Eros in cursus turpis massa tincidunt dui ut ornare. Tristique senectus et netus et malesuada.
```
!pip install -q nxviz
!pip install -q scispacy
!pip install -q https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.4.0/en_ner_bc5cdr_md-0.4.0.tar.gz
```
Let's import required functions
```
import scispacy
import spacy
```
We need to load the NER model 
```
nlp = spacy.load("en_ner_bc5cdr_md")
```
Cras ornare arcu dui vivamus arcu felis bibendum ut tristique. Eget felis eget nunc lobortis mattis. Non pulvinar neque laoreet suspendisse interdum consectetur libero id faucibus. Egestas pretium aenean pharetra magna ac placerat. Amet consectetur adipiscing elit pellentesque habitant morbi tristique. Purus ut faucibus pulvinar elementum integer. Augue eget arcu dictum varius duis.

# Building & Visualising Graphs
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget sit amet tellus cras adipiscing enim eu turpis. 

# Abstract as Network Graph
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget sit amet tellus cras adipiscing enim eu turpis. Sagittis orci a scelerisque purus semper. 

Tempor id eu nisl nunc mi ipsum faucibus vitae. At elementum eu facilisis sed odio morbi quis commodo odio. Eget lorem dolor sed viverra. In dictum non consectetur a erat nam at lectus urna. Imperdiet proin fermentum leo vel orci porta. Eros in cursus turpis massa tincidunt dui ut ornare. Tristique senectus et netus et malesuada.

# MeSH terms as Network Graph
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget sit amet tellus cras adipiscing enim eu turpis. Sagittis orci a scelerisque purus semper. 

Tempor id eu nisl nunc mi ipsum faucibus vitae. At elementum eu facilisis sed odio morbi quis commodo odio. Eget lorem dolor sed viverra. In dictum non consectetur a erat nam at lectus urna. Imperdiet proin fermentum leo vel orci porta. Eros in cursus turpis massa tincidunt dui ut ornare. Tristique senectus et netus et malesuada.

# Conclusion
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget sit amet tellus cras adipiscing enim eu turpis. Sagittis orci a scelerisque purus semper. Tempor id eu nisl nunc mi ipsum faucibus vitae. At elementum eu facilisis sed odio morbi quis commodo odio. Eget lorem dolor sed viverra. In dictum non consectetur a erat nam at lectus urna. Imperdiet proin fermentum leo vel orci porta. Eros in cursus turpis massa tincidunt dui ut ornare. Tristique senectus et netus et malesuada.

# Summary
1. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
2. Eget sit amet tellus cras adipiscing enim eu turpis. Sagittis orci a scelerisque purus semper. 
3. Tempor id eu nisl nunc mi ipsum faucibus vitae. 
4. Cras ornare arcu dui vivamus arcu felis bibendum ut tristique. Eget felis eget nunc lobortis mattis. 
5. Consequat id porta nibh venenatis. Fringilla ut morbi tincidunt augue interdum velit euismod in. Euismod nisi porta lorem mollis aliquam ut porttitor. 

# References



