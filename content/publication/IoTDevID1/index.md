---
title: 'WiFi Based Distance Estimation Using Supervised Machine Learning'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - Kahraman Kostas
  - admin
  - Francisco Zampella
  - Firas Alsehly


date: '2022-08-15T00:00:00Z'
doi: ''

# Schedule page publish date (NOT publication's date).
publishDate: '2022-08-15T00:00:00Z'

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ['3']

# Publication name and optional abbreviated publication name.

abstract:  In recent years WiFi became the primary source of information to locate a person or device indoor. Collecting RSSI values as reference measurements with known positions, known as WiFi fingerprinting, is commonly used in various positioning methods and algorithms that appear in literature. However, measuring the spatial distance between given set of WiFi fingerprints is heavily affected by the selection of the signal distance function used to model signal space as geospatial distance. In this study, the authors proposed utilization of machine learning to improve the estimation of geospatial distance between fingerprints. This research examined data collected from 13 different open datasets to provide a broad representation aiming for general model that can be used in any indoor environment. The proposed novel approach extracted data features by examining a set of commonly used signal distance metrics via feature selection process that includes feature analysis and genetic algorithm. To demonstrate that the output of this research is venue independent, all models were tested on datasets previously excluded during the training and validation phase. Finally, various machine learning algorithms were compared using wide variety of evaluation metrics including ability to scale out the test bed to real world unsolicited datasets.



tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: ''
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
  - example

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
links:
  - icon: github
    icon_pack: fab
    name: Code
    url: https://github.com/kahramankostas/WiFi-Fingerprint
---
