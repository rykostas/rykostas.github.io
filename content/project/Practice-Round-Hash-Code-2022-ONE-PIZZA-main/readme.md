---
title: Practice Round - Hash Code 2022
summary: You are opening a small pizzeria. In fact, your pizzeria is so small that you decided to offer only one type of pizza. Now you need to decide what ingredients to include 
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
    url: https://github.com/kahramankostas/Practice-Round-Hash-Code-2022-ONE-PIZZA
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
# Practice Round - Hash Code 2022

# One Pizza

# Problem

<img src="./img/pizzeria.gif" alt="drawing" style="width:500px;"/>
<img src="./img/pizza-poll.png" alt="drawing" style="width:200px;"/>

You are opening a small pizzeria. In fact, your pizzeria is **so** small that you decided to offer only **one type of pizza**. Now you need to decide what ingredients to include (peppers? tomatoes? both?).

Everyone has their own pizza preferences. Each of your potential clients has some ingredients they like, and maybe some ingredients they dislike. Each client will come to your pizzeria if both conditions are true:

1. **all** the ingredients they like are on the pizza, and
2. **none** of the ingredients they dislike are on the pizza


Each client is OK with additional ingredients they neither like or dislike being present on the pizza. Your task is to choose which ingredients to put on your only pizza type, to maximize the number of clients that will visit your pizzeria.


## Input
* The first line contains one integer 1≤C≤10^5  the number of potential clients.
* The following 2XC lines describe the clients’ preferences in the following format:

    - First line contains integer  1≤L≤5, followed by L names of ingredients a client likes, delimited by spaces.
    - Second line contains integer  0≤D≤5,, followed by D names of ingredients a client dislikes, delimited by spaces.
    
    
Each ingredient name consists of between 1 and 15 ASCII characters. Each character is one of the lowercase letters (a-z) or a digit (0-9).



## Submission
The submission should consist of one line consisting of a single number 0≤N followed by a list of N ingredients to put on the only pizza available in the pizzeria, separated by spaces. The list of ingredients should contain only the ingredients mentioned by at least one client, without duplicates.

## Scoring
A solution scores one point for each client that will come to your pizzeria. A client will come to your pizzeria if **all the ingredients they like** are on the pizza and **none of the ingredients they dislike** are on the pizza.


## Sample
<img src="./img/ornek.jpg" alt="drawing" style="width:800px;"/>


In the Sample Input there are 3 potential clients:

* The first client likes 2 ingredients, cheese and peppers, and does not dislike anything.
* The second client likes only basil and dislikes only pineapple.
* The third client likes mushrooms and tomatoes and dislikes only basil


The picture below shows the preferences of 3 potential clients.
<img src="./img/pizza-poll-examples.png" alt="drawing" style="width:800px;"/>


In this particular Sample Output, we choose to use 4 ingredients in the pizza: cheese, mushrooms, tomatoes, and peppers.

<img src="./img/pizza-sample-output.png" alt="drawing" style="width:400px;"/>


* The first client likes the pizza because it contains both cheese and peppers, which they like.
* The second client does not like the pizza: it does not contain basil which they like.
* The third client likes the pizza because it contains mushrooms and tomatoes, which they like, and does not contain basil which they do not like.



This means a submission of this output would score 2 points for this case, because two clients (the first and third ones) would like this pizza.

<center><h1>Solutions</h1></center>




```python
import os
```

#### folder creation function.  creates the folders to put the outputs.


```python
def folder(f_name): 
    try:
        if not os.path.exists(f_name):
            os.makedirs(f_name)
    except OSError:
        print ("Tthe folder could not be created!")
```

#### The function that finds the locations of required files


```python

def find_the_way(path,file_format):
    files_add = []
    # r=root, d=directories, f = files
    for r, d, f in os.walk(path):
        for file in f:
            if file_format in file:
                files_add.append(os.path.join(r, file))  
    return files_add
files_add=find_the_way('./input/','.txt')
```

#### This Function evaluates the results obtained. as output, it gives you how many people can eat the pizza you created.


```python
def evaluate(outputfolder):
    total=0
    flag=0
    for myfile in files_add:
        like=[]
        dislike=[]
        counter=0
        person=0
        output_filename=outputfolder+myfile[8:]
        with open(output_filename, "r") as file:
            output=file.readline()
        output=output.split(" ")
        output=output[1:]
        with open(myfile, "r") as file:
            while True:
                line=file.readline()
                if line=="":break
                if counter!=0:
                    line=line.replace("\n","")
                    line=line.split(" ")
                        
                        
                    if counter%2!=0:
                        temp1=1
                        for i in line[1:]:
                            if i not in output:
                                temp1=0
                                
                    if counter%2==0:
                        temp2=1
                        for i in line[1:]:
                            if i in output:
                                temp2=0  
                        
                        person+=(temp1 and temp2)                                 
                
                counter+=1
        print('%-15s %-30s %-10s %-10s' % ("File name: ",str(myfile)," score:",  str(person) ))
            


        total=total+person
    print(f'Total score: {total}')
```

#### Input File List


```python
files_add
```




    ['./input/a_an_example.in.txt',
     './input/b_basic.in.txt',
     './input/c_coarse.in.txt',
     './input/d_difficult.in.txt',
     './input/e_elaborate.in.txt']



# VERSION 1

The first and simplest method that comes to mind is to bring together all the desired and unwanted materials in separate lists, and then remove the unwanted materials from the desired list.

This method has been followed in version 1.


```python
outputfolder="outputV1/"
folder(outputfolder)
for myfile in files_add:
    like=[]
    dislike=[]
    counter=0
    with open(myfile, "r") as file:
        while True:
            line=file.readline()
            if line=="":break
            if counter!=0:
                line=line.replace("\n","")
                #print(line,counter)
                line=line.split(" ")
                if counter%2==0:
                    for i in line[1:]:
                        if i not in dislike:
                            dislike.append(i)
      
                else:
                    for i in line[1:]:
                        if i not in like:
                            like.append(i)
            counter+=1
    for i in dislike:
        try:
            like.remove(i)
        except:pass
    temp=(" ".join( i for i in like ))
    temp=str(len(like))+" "+temp
    output_filename=outputfolder+myfile[8:]
    ths = open(output_filename, "w")
    ths.write(temp)
    ths.close()
```

#### Evaluation of version 1


```python
evaluate(outputfolder)
```

    File name:      ./input/a_an_example.in.txt     score:    2         
    File name:      ./input/b_basic.in.txt          score:    5         
    File name:      ./input/c_coarse.in.txt         score:    1         
    File name:      ./input/d_difficult.in.txt      score:    1420      
    File name:      ./input/e_elaborate.in.txt      score:    412       
    Total score: 1840
    

# VERSION 2

#### We never mentioned how many times the materials were repeated in the first version. However, this is very important information.


#### In this version, the number of repetitions of all the liked and disliked material is kept in a dictionary. If the number of repetitions of an item in the list of disliked items is greater than the number of repetitions in the list of liked items, that item is removed from the list. Otherwise (if the number of likes is higher than the number of dislikes) it is kept in the list.


```python
outputfolder="outputV2/"
folder(outputfolder)
for myfile in files_add:
    
    like=[]
    dislike=[]
    counter=0
    hist_like = {}
    hist_dislike = {}
    with open(myfile, "r") as file:
        while True:
            line=file.readline()
            if line=="":break
            if counter!=0:
                line=line.replace("\n","")
                line=line.split(" ")
                if counter%2==0:
                    for i in line[1:]:
                        hist_dislike[i] = hist_dislike.get(i, 0) + 1
                        if i not in dislike:
                            dislike.append(i)
                else:
                    for i in line[1:]:
                        hist_like[i] = hist_like.get(i, 0) + 1
                        if i not in like:
                            like.append(i)
            counter+=1
            
    for i in dislike:
        try:
            if hist_like[i]>hist_dislike[i]:
                pass
            else:
                like.remove(i) 
        except:pass
        
        
    temp=(" ".join( i for i in like ))
    temp=str(len(like))+" "+temp
    output_filename=outputfolder+myfile[8:]
    ths = open(output_filename, "w")
    ths.write(temp)
    ths.close()
    print(myfile)
    hist_like={k: v for k, v in sorted(hist_like.items(), key=lambda item: item[1])}
    #print("\n\n\n\n\nLikes:",hist_like)
    hist_dislike={k: v for k, v in sorted(hist_dislike.items(), key=lambda item: item[1])}
    #print("\nDisLikes:",hist_dislike)


```

    ./input/a_an_example.in.txt
    ./input/b_basic.in.txt
    ./input/c_coarse.in.txt
    ./input/d_difficult.in.txt
    ./input/e_elaborate.in.txt
    

#### Evaluation of version 2


```python
evaluate(outputfolder)
```

    File name:      ./input/a_an_example.in.txt     score:    2         
    File name:      ./input/b_basic.in.txt          score:    5         
    File name:      ./input/c_coarse.in.txt         score:    4         
    File name:      ./input/d_difficult.in.txt      score:    1697      
    File name:      ./input/e_elaborate.in.txt      score:    799       
    Total score: 2507
    

# VERSION 3

#### Another feature that we will add in the last step is to reduce the influence of overly selective customers. For example, if a customer doesn't like an ingredient, it may be wise to remove that ingredient from our list to gain that customer. however, if a customer doesn't like 10 materials, it will be wiser to ignore that customer or reduce their influence.

#### In this step, we have added a method that reduces the impact of such customers. While adding the number of disliked items, we divided this number by how many items the customer disliked.

#### For example, if customer A dislikes tomato, mushrooms and bacon, we add 1/3 point from here to the dislike value of tomato (tomato/length of customer A's dislike list). If customer B only doesn't like the tomato then we add 1 point to the dislike value of the tomato (tomato/length of customer B's dislike list).


```python
outputfolder="outputV3/"
folder(outputfolder)


for myfile in files_add:
    
    like=[]
    dislike=[]
    counter=0
    hist_like = {}
    hist_dislike = {}
    with open(myfile, "r") as file:
        while True:
            line=file.readline()
            if line=="":break
            if counter!=0:
                line=line.replace("\n","")
                line=line.split(" ")
                if counter%2==0:
                    for i in line[1:]:
                        hist_dislike[i] = hist_dislike.get(i, 0) + 1/len(line[1:])
                        if i not in dislike:
                            dislike.append(i)
                else:
                    for i in line[1:]:
                        hist_like[i] = hist_like.get(i, 0) + 1
                        if i not in like:
                            like.append(i)
            counter+=1
            
    for i in dislike:
        try:
            if hist_like[i]>hist_dislike[i]:
                pass
            else:
                like.remove(i) 
        except:pass
        
        
    temp=(" ".join( i for i in like ))
    temp=str(len(like))+" "+temp
    output_filename=outputfolder+myfile[8:]
    ths = open(output_filename, "w")
    ths.write(temp)
    ths.close()
    print(myfile)
    hist_like={k: v for k, v in sorted(hist_like.items(), key=lambda item: item[1])}
    #print("\n\n\n\n\nLikes:",hist_like)
    hist_dislike={k: v for k, v in sorted(hist_dislike.items(), key=lambda item: item[1])}
    #print("\nDisLikes:",hist_dislike)


# In[53]:

```

    ./input/a_an_example.in.txt
    ./input/b_basic.in.txt
    ./input/c_coarse.in.txt
    ./input/d_difficult.in.txt
    ./input/e_elaborate.in.txt
    


```python
evaluate(outputfolder)
```

    File name:      ./input/a_an_example.in.txt     score:    2         
    File name:      ./input/b_basic.in.txt          score:    5         
    File name:      ./input/c_coarse.in.txt         score:    4         
    File name:      ./input/d_difficult.in.txt      score:    1480      
    File name:      ./input/e_elaborate.in.txt      score:    1247      
    Total score: 2738
    
