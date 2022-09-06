---
title: World name statistics
summary: forenames and statistics by country
tags:
  - Deep Learning
date: '2022-04-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

links:
  - icon: twitter
    icon_pack: fab
    name: Follow
    url: https://twitter.com/kkostas
  - icon: github
    icon_pack: fab
    name: Github
    url: https://github.com/kahramankostas/Name-statistics-by-country-in-the-world
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
---
# World name statistics

# forenames and statistics by country

## Creating a dataset of forenames by country using Web Crawling.

### This code extracted the forenames and their gender (number of males and females carrying the name), number and frequency of use from the [forebears.io](https://forebears.io/) website and saved them in a ``` CSV``` file for each country.



### The view of the generated files is as follows (Country: Turkey)

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Male</th>
      <th>Female</th>
      <th>Incidence</th>
      <th>Frequency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mehmet</td>
      <td>100</td>
      <td>0</td>
      <td>2557203</td>
      <td>1:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Fatma</td>
      <td>0</td>
      <td>100</td>
      <td>1808748</td>
      <td>1:43</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mustafa</td>
      <td>100</td>
      <td>0</td>
      <td>1461828</td>
      <td>1:53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ayşe</td>
      <td>0</td>
      <td>100</td>
      <td>1413659</td>
      <td>1:55</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ahmet</td>
      <td>100</td>
      <td>0</td>
      <td>1254943</td>
      <td>1:62</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>Pembe</td>
      <td>0</td>
      <td>100</td>
      <td>9488</td>
      <td>1:8200</td>
    </tr>
    <tr>
      <th>996</th>
      <td>Sevdiye</td>
      <td>0</td>
      <td>100</td>
      <td>9458</td>
      <td>1:8226</td>
    </tr>
    <tr>
      <th>997</th>
      <td>Gürbüz</td>
      <td>96</td>
      <td>4</td>
      <td>9448</td>
      <td>1:8235</td>
    </tr>
    <tr>
      <th>998</th>
      <td>Amine</td>
      <td>0</td>
      <td>100</td>
      <td>9438</td>
      <td>1:8243</td>
    </tr>
    <tr>
      <th>999</th>
      <td>Şemse</td>
      <td>0</td>
      <td>100</td>
      <td>9420</td>
      <td>1:8259</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>




```
# required modules
import re
import codecs
from urllib.request import Request, urlopen
```

## Alphabetical list of scanned countries


```
countrys=["afghanistan",
"albania",
"algeria",
"andorra",
"angola",
"antigua-and-barbuda",
"argentina",
"armenia",
"australia",
"austria",
"azerbaijan",
"bahamas",
"bahrain",
"bangladesh",
"barbados",
"belarus",
"belgium",
"belize",
"benin",
"bhutan",
"bolivia",
"bosnia-and-herzegovina",
"botswana",
"brazil",
"brunei",
"bulgaria",
"burkina-faso",
"burundi",
#"côte-d'ivoire",
"cabo-verde",
"cambodia",
"cameroon",
"canada",
"central-african-republic",
"chad",
"chile",
"china",
"colombia",
"comoros",
"congo","congo-brazzaville",
"costa-rica",
"croatia",
"cuba",
"cyprus",
"czechia","czech-republic",
"democratic-republic-of-the-congo",
"denmark",
"djibouti",
"dominica",
"dominican-republic",
"ecuador",
"egypt",
"el-salvador",
"equatorial-guinea",
"eritrea",
"estonia",
"eswatini","swaziland",
"ethiopia",
"fiji",
"finland",
"france",
"gabon",
"gambia",
"georgia",
"germany",
"ghana",
"greece",
"grenada",
"guatemala",
"guinea",
"guinea-bissau",
"guyana",
"haiti",
"holy-see",
"honduras",
"hungary",
"iceland",
"india",
"indonesia",
"iran",
"iraq",
"ireland",
"israel",
"italy",
"jamaica",
"japan",
"jordan",
"kazakhstan",
"kenya",
"kiribati",
"kuwait",
"kyrgyzstan",
"laos",
"latvia",
"lebanon",
"lesotho",
"liberia",
"libya",
"liechtenstein",
"lithuania",
"luxembourg",
"madagascar",
"malawi",
"malaysia",
"maldives",
"mali",
"malta",
"marshall-islands",
"mauritania",
"mauritius",
"mexico",
"micronesia",
"moldova",
"monaco",
"mongolia",
"montenegro",
"morocco",
"mozambique",
"myanmar-(formerly-burma)",
"namibia",
"nauru",
"nepal",
"netherlands",
"new-zealand",
"nicaragua",
"niger",
"nigeria",
"north-korea",
"north-macedonia",
"norway",
"oman",
"pakistan",
"palau",
"palestine-state",
"panama",
"papua-new-guinea",
"paraguay",
"peru",
"philippines",
"poland",
"portugal",
"qatar",
"romania",
"russia",
"rwanda",
"saint-kitts-and-nevis",
"saint-lucia",
"saint-vincent-and-the-grenadines",
"samoa",
"san-marino",
"sao-tome-and-principe",
"saudi-arabia",
"senegal",
"serbia",
"seychelles",
"sierra-leone",
"singapore",
"slovakia",
"slovenia",
"solomon-islands",
"somalia",
"south-africa",
"south-korea",
"south-sudan",
"spain",
"sri-lanka",
"sudan",
"suriname",
"sweden",
"switzerland",
"syria",
"tajikistan",
"tanzania",
"thailand",
"timor-leste",
"togo",
"tonga",
"trinidad-and-tobago",
"tunisia",
"turkey",
"turkmenistan",
"tuvalu",
"uganda",
"ukraine",
"united-arab-emirates",
"united-kingdom",
"united-states-of-america",
"uruguay",
"uzbekistan",
"vanuatu",
"venezuela",
"vietnam",
"yemen",
"zambia",
"zimbabwe"]
```


```
header="Name,Male,Female,Incidence,Frequency\n"
for country in countrys:
    try:
        site="https://forebears.io/"+country+"/forenames"
        req = Request(site, headers={'User-Agent': 'Mozilla/5.0'})
        webpage = urlopen(req,timeout=10).read()

        s=webpage.decode("utf-8")



        a="Frequency</th></tr></thead><tbody>"
        z="</tbody>"
        start=s.find(a)+len(a)
        stop=s.find(z)


        s1=s[start:stop]
        s1=s1.split("<tr><td>")
        cn=country+".csv"
        ths = codecs.open(cn, "w", "utf-8")
        ths.write(header)  
        
        for i in s1[1:]:
            #Frequency
            result = re.search('%">(.*)</span>', i)
            Frequency=result.group(1)
            Frequency=Frequency.replace(",","")

            #Forename
            result = re.search('forenames/(.*)</a></td>', i)
            result=result.group(1)
            result=result.split(">")
            Forename=result[1]

            #Incidence
            result = re.search('</a></td><td>(.*)</td><td><span', i)
            Incidence=result.group(1)
            Incidence=Incidence.replace(",","")



            #gender and ratio
            try:
                if ">100%<" in i:
                    result = re.search('class="(.*)" style=', i)
                    result=result.group(1)
                    #print(result)
                    if result=="f":
                        female=100
                        male=0
                    else:
                        female=0
                        male=100
                else:
                    result = re.search('"width:(.*)px;', i)
                    result=result.group(1)
                    key1="px"
                    key2="width"
                    start=result.find(key1)
                    stop=result.find(key2)+len(key2)+1
                    male=result[:start]
                    female=result[stop:]
            except:
                male=0
                female=0
            line=[Forename,male,female,Incidence,Frequency]
    
            line=str(line).replace("[","")
            line=str(line).replace("]","")
            line=str(line).replace(", ",",")
            line=str(line).replace("\'","")
            ths.write(str(line)+"\n")  
        ths.close()
        print("OK :", country)
    except:
        print("Error:", country )
```

    OK : afghanistan
    OK : albania
    OK : algeria
    OK : andorra
    OK : angola
    OK : antigua-and-barbuda
    OK : argentina
    OK : armenia
    OK : australia
    OK : austria
    OK : azerbaijan
    OK : bahamas
    OK : bahrain
    OK : bangladesh
    OK : barbados
    OK : belarus
    OK : belgium
    OK : belize
    OK : benin
    OK : bhutan
    OK : bolivia
    OK : bosnia-and-herzegovina
    OK : botswana
    OK : brazil
    OK : brunei
    OK : bulgaria
    OK : burkina-faso
    OK : burundi
    Error: côte-d'ivoire
    OK : cabo-verde
    OK : cambodia
    OK : cameroon
    OK : canada
    OK : central-african-republic
    OK : chad
    OK : chile
    OK : china
    OK : colombia
    OK : comoros
    OK : congo
    OK : congo-brazzaville
    OK : costa-rica
    OK : croatia
    OK : cuba
    OK : cyprus
    OK : czechia
    OK : czech-republic
    OK : democratic-republic-of-the-congo
    OK : denmark
    OK : djibouti
    OK : dominica
    OK : dominican-republic
    OK : ecuador
    OK : egypt
    OK : el-salvador
    OK : equatorial-guinea
    OK : eritrea
    OK : estonia
    OK : eswatini
    OK : swaziland
    OK : ethiopia
    OK : fiji
    OK : finland
    OK : france
    OK : gabon
    OK : gambia
    OK : georgia
    OK : germany
    OK : ghana
    OK : greece
    OK : grenada
    OK : guatemala
    OK : guinea
    OK : guinea-bissau
    OK : guyana
    OK : haiti
    OK : holy-see
    OK : honduras
    OK : hungary
    OK : iceland
    OK : india
    OK : indonesia
    OK : iran
    OK : iraq
    OK : ireland
    OK : israel
    OK : italy
    OK : jamaica
    OK : japan
    OK : jordan
    OK : kazakhstan
    OK : kenya
    OK : kiribati
    OK : kuwait
    OK : kyrgyzstan
    OK : laos
    OK : latvia
    OK : lebanon
    OK : lesotho
    OK : liberia
    OK : libya
    OK : liechtenstein
    OK : lithuania
    OK : luxembourg
    OK : madagascar
    OK : malawi
    OK : malaysia
    OK : maldives
    OK : mali
    OK : malta
    OK : marshall-islands
    OK : mauritania
    OK : mauritius
    OK : mexico
    OK : micronesia
    OK : moldova
    OK : monaco
    OK : mongolia
    OK : montenegro
    OK : morocco
    OK : mozambique
    OK : myanmar-(formerly-burma)
    OK : namibia
    OK : nauru
    OK : nepal
    OK : netherlands
    OK : new-zealand
    OK : nicaragua
    OK : niger
    OK : nigeria
    OK : north-korea
    OK : north-macedonia
    OK : norway
    OK : oman
    OK : pakistan
    OK : palau
    OK : palestine-state
    OK : panama
    OK : papua-new-guinea
    OK : paraguay
    OK : peru
    OK : philippines
    OK : poland
    OK : portugal
    OK : qatar
    OK : romania
    OK : russia
    OK : rwanda
    OK : saint-kitts-and-nevis
    OK : saint-lucia
    OK : saint-vincent-and-the-grenadines
    OK : samoa
    OK : san-marino
    OK : sao-tome-and-principe
    OK : saudi-arabia
    OK : senegal
    OK : serbia
    OK : seychelles
    OK : sierra-leone
    OK : singapore
    OK : slovakia
    OK : slovenia
    OK : solomon-islands
    OK : somalia
    OK : south-africa
    OK : south-korea
    OK : south-sudan
    OK : spain
    OK : sri-lanka
    OK : sudan
    OK : suriname
    OK : sweden
    OK : switzerland
    OK : syria
    OK : tajikistan
    OK : tanzania
    OK : thailand
    OK : timor-leste
    OK : togo
    OK : tonga
    OK : trinidad-and-tobago
    OK : tunisia
    OK : turkey
    OK : turkmenistan
    OK : tuvalu
    OK : uganda
    Error: ukraine
    OK : united-arab-emirates
    OK : united-kingdom
    OK : united-states-of-america
    OK : uruguay
    OK : uzbekistan
    OK : vanuatu
    OK : venezuela
    OK : vietnam
    OK : yemen
    OK : zambia
    OK : zimbabwe
    
