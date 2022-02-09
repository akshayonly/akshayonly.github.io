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

![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/2.png "Image_shadow"){:.shadow}
<br>
![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/3.png "Image_shadow"){:.shadow}


Forming such a network connection helps us understand relationships between entities. Apart from visualizing interconnected notes, such network-graph or graphs have actual scientific use cases. The image below displays the protein interactome-based study of schizophrenia, and another image displays the network analysis and visualization of political blogs preceding the U.S. Presidential Election of 2004.

![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/4.png "Image_shadow"){:.shadow}
<br>
![Image](https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/Post-01-Imgs/5.png "Image_shadow"){:.shadow}

This let me ponder upon different possibilities. I thought, wouldn’t it would be great if we can represent a scientific article (or biomedical literature) in a graph manner? But why should anyone visualize scientific literature as a network graph? Simple answer, for getting a high-level overview of relevant terms before jumping into reading the article.

But how can we do this? I started researching (googling) whether such tools or platforms exist. I came across connected papers, this site builds graphs of related papers based on the user-given paper. Cool visualization, but not what we want. So let's build our own tool but this isn’t straightforward also, there are a few issues here:

1. Not all biomedical articles or literature is accessible. i.e., paywalls.
2. Even if we get articles that are accessible, processing on average 6-9 pages of PDFs can be a little tricky.
3. Also, if we scale up to incorporate many articles this can prove challenging. Because there can be different words with similar meanings. 

So to tackle the above issues and to keep hands simple we'd use MeSH terms which are present for most of the biomedical literature. (We'd learn more about them below)
