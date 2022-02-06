---
layout: article
title:  "Visualizing MeSH terms as a Network Graph"
tags: MeSH PubMed E-utilities Biopython Pyvis
aside:
  toc: false
mode: immersive
header:
  theme: dark
article_header:
  type: cover
  image:
    src: assets/post-imgs/p1-header-img-01-resize.png
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

Recently I switched to Obsidian as a primary notes-taking platform. Obsidian has an amazing feature that lets the user view their notes as a graph. Below is a snapshot of my notes. 

<div class="swiper my-3 swiper-demo swiper-demo--image swiper-demo--3">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/post-imgs/p1-screenshoot-01.jpg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://raw.githubusercontent.com/akshayonly/akshayonly.github.io/master/assets/post-imgs/p1-screenshoot-02.jpg"/></div>
  </div>
  <div class="swiper__button swiper__button--prev fas fa-chevron-left"></div>
  <div class="swiper__button swiper__button--next fas fa-chevron-right"></div>
</div>
<script>
{%- include scripts/lib/swiper.js -%}
var SOURCES = window.TEXT_VARIABLES.sources;
window.Lazyload.js(SOURCES.jquery, function() {
  $('.swiper-demo').swiper();
});
</script>

This let me ponder upon possibilities to put in place such a structure for biomedical literature. I thought, wouldn’t it would be great if we can represent a research article in a graph manner? Upon researching (googling...) I came across [connected papers](https://www.connectedpapers.com/), this site builds graphs of related papers based on the user-given paper. 

Cool visualization, but I wanted to visualize a research article as a network graph. This isn't straightforward also, there are a few issues here:
1. Not all biomedical articles or literature is available. i.e., paywalls.
2. Processing the entire text in typical 6-8 pages literature is non-trivial.
3. Even if we processed the text, there can be different terms for the single biomedical phenomenon. This can create an issue if we scaled up our ‘graph-based visualizer’ to incorporate multiple articles. Because one article can have 'cancer' term, while another can have 'neoplasm'. Hence, then connecting such two terms which have similar meanings would be challenging.

So to simplify the approach, I decided to use MeSH terms which are available for most of the biomedical articles present in PubMed.

# Handling millions of biomedical citations

PubMed is a search engine-like resource that provides access to biomedical and life sciences literature. In another word, it’d a freely available database that stores more than 33 million citations and abstracts of biomedical literature. Now searching through millions of records and retrieval of specific literature based on user-given queries or topics can be challenging. If the query is about ‘Cancer’, you don’t want to return information related to some other disease like ‘Malaria’. Also, terms such as ‘Neoplasm’, ‘Tumour’ and ‘Cancer’ are umbrella terms, so in order to deal with such and more issues, the Medical Subject Headings (MeSH) were introduced. 

# 20 Cancer pubmed articles & Covid-19 pubmed articles MeSH terms network graph
<div>{%- include extensions/youtube.html id='Op4RV-kaTxk' -%}</div>

# Primer on Graph theory with pyvis

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla risus leo, aliquam quis metus et, luctus facilisis mauris. Nam iaculis laoreet diam, quis viverra nisi varius et. Suspendisse viverra orci orci, iaculis iaculis tortor consectetur non. Vestibulum tincidunt, tortor eget scelerisque feugiat, massa sem interdum diam, at tincidunt erat orci ac erat. Fusce at luctus lacus, et ultricies odio. Aenean rutrum ligula vitae vestibulum ullamcorper. Integer vitae dignissim orci. Nullam at mattis ligula. Integer tempus turpis porta nibh ullamcorper cursus.

~~~ python
! pip install -q pyvis
~~~

Sed at accumsan velit. Vestibulum congue pharetra urna id rutrum. Fusce sapien libero, posuere non urna ut, facilisis sodales orci. Aenean consequat lacinia erat. Nullam semper eros sed tortor tempus semper. Proin suscipit, massa at ultricies tristique, arcu metus varius sapien, id imperdiet metus erat nec velit. Mauris a nisi vitae nisl interdum pellentesque. Maecenas vel facilisis nulla. Praesent tortor odio, eleifend a rutrum vitae, dignissim in felis.

~~~ python
from pyvis.network import Network
~~~

Nam elementum non nulla eget viverra. Integer egestas ipsum risus, vel ornare est tincidunt quis. Nulla sit amet tortor sed magna consequat dapibus. Proin ullamcorper lacus id feugiat tincidunt. Sed sed diam erat. Maecenas nec odio vitae mi varius lobortis. Donec ultrices libero eget massa accumsan suscipit. Aliquam erat volutpat. Phasellus ut libero a leo sagittis rutrum ut in enim. Suspendisse massa dolor, blandit at magna a, tristique sollicitudin tortor. Praesent non tincidunt neque. Quisque vel auctor lacus, vel vulputate tellus. Curabitur a tristique arcu. In imperdiet, nisi ut tristique feugiat, massa sapien sodales risus, eget accumsan ipsum metus quis est. Sed nisl lacus, ornare at ante vulputate, suscipit dapibus risus.


## Dummy Title 01

The standard Lorem Ipsum passage, used since the 1500s “Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 

~~~ python
def fetch_data(pmids):
    """Returns pubmed record associated with the PMID(s)"""
    
    Entrez.email = 'yourmailid@mail.com'

    handle = Entrez.efetch(db="pubmed", 
                           id=pmids, 
                           rettype="medline", 
                           retmode="text")

    records = Medline.parse(handle)    
    
    return list(records)
~~~

Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.”


## Dummy Title 02
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla risus leo, aliquam quis metus et, luctus facilisis mauris. Nam iaculis laoreet diam, quis viverra nisi varius et. Suspendisse viverra orci orci, iaculis iaculis tortor consectetur non. Vestibulum tincidunt, tortor eget scelerisque feugiat, massa sem interdum diam, at tincidunt erat orci ac erat. Fusce at luctus lacus, et ultricies odio. Aenean rutrum ligula vitae vestibulum ullamcorper. Integer vitae dignissim orci. Nullam at mattis ligula. Integer tempus turpis porta nibh ullamcorper cursus.

~~~ python
Entrez.email = 'yourmailid@mail.com'

handle = Entrez.efetch(db="pubmed", 
                       id=pmids, 
                       rettype="medline", 
                       retmode="text")

records = Medline.parse(handle)    
~~~

~~~ python
print(handle.read())
~~~

## Dummy Title 03

Sed at accumsan velit. Vestibulum congue pharetra urna id rutrum. Fusce sapien libero, posuere non urna ut, facilisis sodales orci. Aenean consequat lacinia erat. Nullam semper eros sed tortor tempus semper. Proin suscipit, massa at ultricies tristique, arcu metus varius sapien, id imperdiet metus erat nec velit. Mauris a nisi vitae nisl interdum pellentesque. Maecenas vel facilisis nulla. Praesent tortor odio, eleifend a rutrum vitae, dignissim in felis.

~~~ python
print(handle.read())
~~~

~~~ 
PMID- 32720228
OWN - NLM
STAT- MEDLINE
DCOM- 20210527
LR  - 20210527
IS  - 0948-5023 (Electronic)
IS  - 0948-5023 (Linking)
VI  - 26
~~~

## Dummy Title 03
Sed at accumsan velit. Vestibulum congue pharetra urna id rutrum. Fusce sapien libero, posuere non urna ut, facilisis sodales orci. Aenean consequat lacinia erat. Nullam semper eros sed tortor tempus semper. 

~~~ python
records = Medline.parse(handle)  
~~~

Proin suscipit, massa at ultricies tristique, arcu metus varius sapien, id imperdiet metus erat nec velit. Mauris a nisi vitae nisl interdum pellentesque. Maecenas vel facilisis nulla. Praesent tortor odio, eleifend a rutrum vitae, dignissim in felis.
~~~ python
print(type(records), records)
~~~

~~~
<class 'generator'> <generator object parse at 0x7f414d45d1d0>
~~~

## Dummy Title 06
Proin suscipit, massa at ultricies tristique, arcu metus varius sapien, id imperdiet metus erat nec velit. Mauris a nisi vitae nisl interdum pellentesque. Maecenas vel facilisis nulla. Praesent tortor odio, eleifend a rutrum vitae, dignissim in felis.

Nam elementum non nulla eget viverra. Integer egestas ipsum risus, vel ornare est tincidunt quis. Nulla sit amet tortor sed magna consequat dapibus. Proin ullamcorper lacus id feugiat tincidunt. Sed sed diam erat. Maecenas nec odio vitae mi varius lobortis. Donec ultrices libero eget massa accumsan suscipit. Aliquam erat volutpat. Phasellus ut libero a leo sagittis rutrum ut in enim. Suspendisse massa dolor, blandit at magna a, tristique sollicitudin tortor. Praesent non tincidunt neque. Quisque vel auctor lacus, vel vulputate tellus. Curabitur a tristique arcu. In imperdiet, nisi ut tristique feugiat, massa sapien sodales risus, eget accumsan ipsum metus quis est. Sed nisl lacus, ornare at ante vulputate, suscipit dapibus risus.

~~~ python
MKGraph = Network(height='750px', width='100%', bgcolor='#ecf0f1', font_color='#1e272e', notebook=True)
~~~

~~~ python
MKGraph.set_options("""
var options = {
  "edges": {
    "arrows": {
      "to": {
        "enabled": true,
        "scaleFactor": 0.5
      }
    },
    "color": {
      "inherit": true
    },
    "smooth": {
      "forceDirection": "none"
    }
  },
  "physics": {
    "barnesHut": {
      "gravitationalConstant": -17350,
      "springLength": 210,
      "springConstant": 0.055,
      "avoidOverlap": 0.53
    },
    "minVelocity": 0.75
  }
}
""")
~~~

Nam elementum non nulla eget viverra. Integer egestas ipsum risus, vel ornare est tincidunt quis. Nulla sit amet tortor sed magna consequat dapibus. Proin ullamcorper lacus id feugiat tincidunt. Sed sed diam erat. Maecenas nec odio vitae mi varius lobortis. Donec ultrices libero eget massa accumsan suscipit. Aliquam erat volutpat. Phasellus ut libero a leo sagittis rutrum ut in enim. Suspendisse massa dolor, blandit at magna a, tristique sollicitudin tortor. Praesent non tincidunt neque. Quisque vel auctor lacus, vel vulputate tellus. Curabitur a tristique arcu. In imperdiet, nisi ut tristique feugiat, massa sapien sodales risus, eget accumsan ipsum metus quis est. Sed nisl lacus, ornare at ante vulputate, suscipit dapibus risus.

~~~ python
colors = ["#0c2461", "#4a69bd", '#6a89cc', '#f7b731']


mesh_terms = data_dict.get('MH')

if isinstance(mesh_terms, list):

    main_node = f"PMID_{data_dict.get('PMID')}"
    MKGraph.add_node(main_node, size=35, title=data_dict.get('TI'), color=colors[0])

    for terms in mesh_terms:
        temp_list = [term.replace('*', '').replace(',', '').strip() for term in terms.split('/')]

        primary_node = temp_list[0]
        secondary_nodes =  temp_list[1:]

        MKGraph.add_node(primary_node, size=25, color=colors[1])
        MKGraph.add_edge(main_node, primary_node)

        for node in secondary_nodes:
          node = node.title()
          if node in mesh_qualifier_names:
            MKGraph.add_node(node, size=15, color=colors[3])
            MKGraph.add_edge(primary_node, node)
          else:
            MKGraph.add_node(node, size=15, color=colors[2])
            MKGraph.add_edge(primary_node, node)            
else:
    main_node = f"PMID_{data_dict.get('PMID')}"
    primary_node = 'NO_MESH'

    MKGraph.add_node(main_node, size=35, title=data_dict.get('TI'), color='#009432')
    MKGraph.add_node(primary_node, size=25, title='NO MESH TERMS AVAILABLE', color='#EE5A24')

    MKGraph.add_edge(main_node, primary_node)  
~~~

Nam elementum non nulla eget viverra. Integer egestas ipsum risus, vel ornare est tincidunt quis. Nulla sit amet tortor sed magna consequat dapibus. Proin ullamcorper lacus id feugiat tincidunt. Sed sed diam erat. Maecenas nec odio vitae mi varius lobortis. Donec ultrices libero eget massa accumsan suscipit. Aliquam erat volutpat. 

~~~ python
MKGraph.show('single_article_mesh_graph_network.html')
~~~

Phasellus ut libero a leo sagittis rutrum ut in enim. Suspendisse massa dolor, blandit at magna a, tristique sollicitudin tortor. Praesent non tincidunt neque. Quisque vel auctor lacus, vel vulputate tellus. Curabitur a tristique arcu. In imperdiet, nisi ut tristique feugiat, massa sapien sodales risus, eget accumsan ipsum metus quis est. Sed nisl lacus, ornare at ante vulputate, suscipit dapibus risus.

<p class="codepen" data-height="300" data-theme-id="light" data-default-tab="result" data-slug-hash="RwLYywp" data-preview="true" data-user="akshayonly" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/akshayonly/pen/RwLYywp">
  MeSH Terms Network Graph For Single Article - 100width</a> by Akshay Shirsath (<a href="https://codepen.io/akshayonly">@akshayonly</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
