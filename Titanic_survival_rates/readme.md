## Machine Learning Solution of Titanic Problem

### Problem Description  

It a problem in Kaggle, about the Titanic disaster. Given some basic data of all the people on this ship, we should give a solution to predict a person was survived or not.  

### Description of my solution

Basically this problem is about missing value imputation, features engineering and classifiction. I take five steps to solve this problem.

- DATA EXPLORATION
- MISSING VALUES
- TEST BASIC MODEL
- FEATURE ENGINEERING
- OPTIMISE

----
### DATA EXPLORATION
<center><img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81mx1rqycj30gu0guq44.jpg" width="40%" height="40%" /><img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81myo1v59j30oc0oogm7.jpg" " width="40%" height="40%"  /></center>

There are several missing values, and some features have interesting relationship with 'Survived'. (see details in solution_code.py)

### MISSING VALUES
![](https://tva1.sinaimg.cn/large/006y8mN6gy1g81n29ru0aj317e0f8aas.jpg)
left one is age's distribution, right one is the kde picture.

1. According to the above picture, 'Age' looks like Normal Distribution. There are about 20% missing in age, and here we can simply **use the midean to replace the missing**. It seems not good, and **I will improve this method in later part**. (I also tried to use the ramdom normal distribution to simulate the distribution of 'Age' and repalce the missing, but the result is not good, and not very reasonable).
- Considering the missing value of 'Embarked', there are only 2 missing values. **So we can use the most frequent value to replace missing in 'Embarked'**.
- But the missing in 'Cabin' is too much(more than 70%), I don't have good idea to deal with it, so I **delete the 'Cabin'**.


### TEST BASIC MODEL

After process missing values, we simply use one hot encoding to treat features 'Sex', 'Embarked', and 'Pclass'. Then try basic models.

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g81n6cfjvzj316o0f80ut.jpg)


### FEATURE ENGINEERING
#### Buaket Age
- We have discussed that 'Age' has low relationship with 'Survived'. But in Kernel Density Function, as we can see, 'Age' is an important feature. So if we divided the feature into several parts, the relationship might be enhanced.  
- According to Kernel Density Function of Age. We can find in some part, 'Age' is an effective feature. Hence, we should divided the data in some sections and ensure each section include some 'important part'. So Accodring the picture following, we will use.

#### Create 'Family' features according to 'Sibsp' and 'Parch'
- We can use Kernel Density Function to describe the distribution of a variable. And we find SibSp and Parch are not significant features.
- Then, we consider if creat a varible family (= siblings + parents + children). Because the meaning of Sibsp and Parch are similar, and we can just combine them together. The kde photo shows the combination is better.
- Also, it is better to treat the family as a categorical feature rather than a numerical feature. Because it is hard to say the person with 4 family has something 4 times stronger than a person with 1 'Family'. It is reasonable to think a person with soem 'Family' has some speacial features than a person with no 'Family', like family member would definitely help each other. So I will use bucket to treat the 'Family' have family or not.

<center><img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81nd8xp3aj30l60eoglq.jpg" width="38%" height="38%" />
<img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81ndlp4daj30ks0esmxb.jpg" " width="38%" height="38%"  />
<img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81ndrwy9xj30km0em74g.jpg" " width="38%" height="38%"  /></center>

#### Create a feature 'Title' according to 'Name'
- we can see in name there also a title, like 'Mr',' Miss".
- It can be a meaningful information, beacuse whether married can be a good feature. Also, we can use one hot encoding to process this data easily. As the form shows below, the most frequence title is Mr, Miss, Mrs and Master.
- I notice something interesting: there are people with 'Rev' title are all man and they all dead. 'Rev' may be reverend, the man serverd the god. So they probably sacrificed themselves. And 'Rev' can be a meaningful title, other titles I use 'Other' to represent.
- Also, I find their are 400+ last name in 800+ samples. The people with the same last name probably from the same family, so the one with unique last name may get in ship alone, and it can be a feature.

<center><img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81n8vh7txj30co0ho0sx.jpg" width="30%" height="30%" /><img src ="https://tva1.sinaimg.cn/large/006y8mN6gy1g81naj53bzj30ew07c74b.jpg" " width="30%" height="30%"  /></center>

#### From 'Ticket' generate two features: T Count, Unit Fare
- We can see that there are only 681 unique ticket in 891 samples, so many people used the same ticket to get in to the ship, and that can be a useful feature.
- Also it caused the prices of these tickets are much higher than the normal prices. We can use the fare devided by the number of people hold a same ticket, 'Unit_Fare'.
- And I noticed that there are 15 sample's fare is 0, and they are from 1,2 and 3 Pclass. I believe they are missing values, and use the medain 'Unit_Fare' of each class to replace.
- The range of Unit_Fare is to large, which is not good for logisitic regression, So we can take a log to deal with it.
- T_Count large 2 means they are good friends or a family, so we treat it as a categorical feature. Because they one went out with friends, they might help each other.

#### Pclass_Sex: combine Pclass and Sex
- In the lecture, the professor mentioned that in Class 1 and 2, female have large probability to live, but in class 3, female and male's survived rate is equal.
- So we can combine Pclass and Sex, to generate a Pclass_Sex. '1M' means a male in class 1. '2F' means a female in class 2. Then use One Hot Encoding.

#### New way to replace the missing in Age
- The title give us some information about Age. For example, Mrs will be older than Miss.
- So we can use the median of each Title to replace the missing of Age. (an interesting thing is that Masters are very young)

### OPTIMISE

Pick useful features and optimise parameters of models.

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g81ngb6uf3j30or0lw784.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g81nhxmwvpj318m0ew40h.jpg)
