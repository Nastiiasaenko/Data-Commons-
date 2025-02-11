# Google Data Commons API - Research & Exploration

## **Overview**
Google Data Commons provides a structured and linked data repository that aggregates datasets from various sources and organizes them into a **Knowledge Graph (KG)**. This project demonstrates how to effectively use the **Google Data Commons API** for **data retrieval, exploration, and visualization**. 

The tutorials in this repository provide step-by-step guidance on:
- Understanding **Knowledge Graphs** and their structure.
- Accessing and querying **Google Data Commons** using the **Python API**.
- Retrieving **statistical variables**, **entity relationships**, and **geospatial data**.
- Using **Python and Pandas** to manipulate and analyze data.
- Visualizing **interconnected relationships** in the Knowledge Graph.

---

## **Table of Contents**
- [Installation](#installation)
- [Understanding Data Commons](#understanding-data-commons)
- [Tutorials & Notebooks](#tutorials--notebooks)
- [Concepts & API Methods](#concepts--api-methods)
- [How to Use the Tutorials](#how-to-use-the-tutorials)
- [Example Queries & Code Snippets](#example-queries--code-snippets)
- [Future Enhancements](#future-enhancements)

---

## **Installation**
To get started, install the necessary dependencies:

```bash
pip install datacommons datacommons_pandas pygraphviz
```


If using Google Colab, you may also need:

```bash
!apt-get install -y graphviz libgraphviz-dev pkg-config
!pip install datacommons pygraphviz
```




## Understanding Data Commons

### [Our descriptive presentation of Common Concepts](https://docs.google.com/presentation/d/1cTxp4HvP951GjI8eyAq--MeTdscYBJ6RD-VnGD2CqrU/edit?usp=sharing)

Google **Data Commons** is built as a **Knowledge Graph (KG)**, which organizes information as **nodes (entities)** and **edges (relationships)**. These entities can include:

- Countries, States, and Cities
- Population and Demographic Statistics
- Environmental Data (e.g., Carbon Emissions)
- Economic Indicators (e.g., Median Income, Unemployment Rates)

### **Key Features:**

✅ **Unified Data Model** - Combines multiple datasets into a single knowledge graph.  
✅ **Pre-processed Data** - Eliminates the need for manual cleaning.  
✅ **APIs for Access** - Retrieve structured data programmatically using **Python** or **REST API**.  
✅ **Graph Structure** - Allows relational queries (e.g., "Nearby Places", "Contained In").  

More details: [Google Data Commons](https://datacommons.org/)

## **Tutorials & Notebooks**
This repository contains **three interactive Jupyter Notebooks** demonstrating different aspects of the API:

| Notebook | Description |
|----------|------------|
| **[Data Commons Basics](https://github.com/Nastiiasaenko/Data-Commons-/blob/main/Data_Commons_Tutorial_Draft_v1.ipynb)** | Introduction to the API, retrieving properties, and exploring the graph structure. |
| **[Exploring Interconnectivity](https://github.com/Nastiiasaenko/Data-Commons-/blob/main/Tutorial_blocks.ipynb)** | Advanced queries using `get_triples()`, `get_places_in()`, and visualizing networks. |
| **[Building Emissions Dataset](https://github.com/Nastiiasaenko/Data-Commons-/blob/main/Second_Part_tutorial.ipynb)** | Retrieving environmental data (CO₂ emissions, methane levels) and constructing time-series datasets. |


## **Concepts & API Methods**

This project explores key **Data Commons API methods** related to **Knowledge Graphs**, **statistical variables**, and **geospatial data**.

| **Concept** | **Description** | **Example API Method** |
|------------|---------------|---------------------|
| **Knowledge Graph (KG)** | Graph-based data model storing relationships between entities. | `get_triples(dcids)` |
| **Entity (Node)** | A single object in the KG (e.g., country, city, person). | `get_property_values(dcids, properties)` |
| **DCID (Identifier)** | Unique identifier assigned to each entity. | `"geoId/06"` for California |
| **Relationships (Edges)** | Connections between nodes (e.g., "located in", "nearby"). | `get_triples(['geoId/12'])` |
| **Statistical Variable** | Measurable data points (e.g., population, GDP). | `get_stat_series(place, stat_var)` |
| **Nearby Places** | List of closest geographic locations to a given entity. | `get_places_in([geoId/06], "County")` |
| **Contained In** | Finds parent regions of a given entity. | `get_property_values(['geoId/12'], ['containedInPlace'])` |

---

## **How to Use the Tutorials**

Follow these steps to explore **Google Data Commons** using this repository:

### **1️⃣ Run the First Notebook**
Start with `Data_Commons_Tutorial_Draft_v1.ipynb` to understand the API basics.

```python
import datacommons as dc
dcid = 'geoId/12'  # Florida
properties = dc.get_property_values([dcid], ['name', 'latitude', 'longitude'])
print(properties)

```

This returns:

```python
{"geoId/12": {"name": "Florida", "latitude": 27.994402"}}


```

### **2️⃣ Retrieve Statistical Data**

Use `get_stat_series()` to fetch emissions data for US states.

```python
dc.get_stat_series('geoId/12', 'Annual_Emissions_CarbonDioxide_NonBiogenic')


```
### **3️⃣ Visualize the Knowledge Graph**


Use **NetworkX** to generate a graph of entity relationships.

```python

import networkx as nx
import matplotlib.pyplot as plt

G = nx.DiGraph()
triples = dc.get_triples(['geoId/12'])
for s, p, o in triples['geoId/12']:
    G.add_edge(s, o, label=p)

nx.draw(G, with_labels=True)
plt.show()
```

➡️ (This will generate a graph visualization showing relationships for Florida.)

## References & Documentation
[Data Commons API Docs](https://docs.datacommons.org/api/)

[Knowledge Graph Explorer](https://datacommons.org/browser/)

[Google Data Commons](https://datacommons.org/)



## Future Enhancements
We plan to expand this project with:

✅ Interactive Visualizations - Implement Plotly Dash for real-time data exploration.

✅ Automated Data Collection - Fetch and update emissions data dynamically.

✅ Integration with Google BigQuery - Combine Data Commons with BigQuery for large-scale analysis.

✅ Geospatial Analysis - Use GeoPandas for mapping emissions trends.









