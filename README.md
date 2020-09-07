# Character-Level RNN

In order to gain a better understanding on RNN, I implement a simple character-level RNN based on Andreij Karparthy's [blog post](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) and his [implementation](https://gist.github.com/karpathy/d4dee566867f8291f086) as well as the Neural Network lecture I've taken in summer semester 2020 in KIT. 

The **training** of this RNN is quiet simple:

1. Give the RNN a huge chunk of text
2. Ask it to model the probability distribution of the next character in the sequence given a sequence of previous characters.

At **test** time, we feed a character into the RNN and get a distribution over what characters are likely to come next. We sample from this distribution, and feed it right back in to get the next letter. Repeat this process.

## Training Data

In directory `./data` there're two text files for training:

- **be-water-my-friend.txt**

  A famous philosophy quote from Bruce Lee.

- **steve-jobs-transcript.txt**

  [Prepared text of the Commencement address](https://news.stanford.edu/2005/06/14/jobs-061505/) delivered by Steve Jobs, CEO of Apple Computer and of Pixar Animation Studios, on June 12, 2005.

##  Sample and Loss

For training I used the shorter text file, **be-water-my-friend.txt**.

```
Empty your mind, be formless. Shapeless, like water. 
If you put water into a cup, it becomes the cup. 
You put water into a bottle and it becomes the bottle. 
You put it in a teapot, it becomes the teapot. 
Now, water can flow or it can crash. Be water, my friend.
```

It is quiet short, which contains only 265 characters.

At the very first beginning, loss was high and the sampled text was very messy:

```
----
 EsBuy,s,
doipSEtls h o BsflNdwhodcbrErfbeotEmEoNcsEat
en,iyNE.rp bmas ucpueIwsBEym
BYnB,ciyEnhrYfpr
,anI yaclkwawlYthySBiaeIrc.uSBy oyoatpuhslpho,aYb,N co r.pSmr ibomyBYtoSpiurdretdieNpc
mywnbrroh.msowdhbmeBspdlhI r,.uE.wrpNu S
ebweyat .rnfbrcYuwtYeiobwnIttsIktataSh b.t
lyBnilwiuiEErBkwbwsbkl.EdIh,lEw
ksmSmpoubloSboamrs
Soh
,BhnwklYNalrNiuasnYifbsdN
nre lwtwbm hNStmYuwuIrrtldyEpfirE
pblIpckS
lwhBythwyaYw.NayblYidYoYcdt,By,tfrBsmp tbibuyesn,bellurmIhkhklNkdNoc.IhooldN,.fk
bb
tIfpitksifNihwmrhip.
lIiho,drtcBENB.
f
pw ,rnhdEa
,esI,.i.lemE,hkdSEY aYhNemrf
teYElYheNciSrtEheBIc,SwcYImNBi.ibupueNyYceewweSpNcb.sybfw
eyynoiEusab pEaehyno.phmbwwsayhEnIEbSYwpEpbnbfk
,ukrBidsiriddcky.BopwbiyE,ttfwwNotpthaNuNbraBuwwS
mNuNkIdBeo,a bufwrcE BSotaedtutto,nrsbk..h BBtEEotowY.IrNelEcB,boN
oBh
psIm. hES llaSS cBacebdnNhc.YrfYew.fcic
ampawBYdIElds,StyfcBeoNiYefIYNw ab.obESNyYc biypime IE,mpBleehidmtsB,Ylr.ifNnYwal..,Ieiwb
.Ifsfumeltlunrylysef,.,inkyISfEdslmufNher l sdIIaStcoh,hENlSE.mh .pnSStw
cmuIiSh
oyIawryY,bwtSop.YaYIpm
hr.fs
hk,IcB ouSyudfsooirhusNris,wh..NuhhsbkoYdBImtiya aurhNyStnYlfEco cwBkBmkbyiiBtdiwSnlrcsws.dEhNBf.StY
khd klYmB.d
baYSeuurbd,Ilphp
aY,
lN
cpdriyBfEeBwyaIEl wso rwIisIm  uwdmlehc,mdcdysNkfENSdBrEmbcaBndpm
nBcywIyk,nhedssdwybsym,sattcaYINIrBmSc
wlic
ribSEppyy
f,liamIESfmsmNy,tl
ctIImYtBnSbhoue,muelNt
ub r
EraaNSkakpcudawYbdIimmklIh  SkfasEycwukc,iiYyIIei
cIBESfIdSu.emdme
w pwofmnmiSSnY
Y,ukcryikbb
p laBmsy kpssu

adnamui  fd
cNeilNBiIyb,nko
ni
Yu,wwtelnwybpIbE.rsdnEEiEhhyho 
----
iter 0, loss: 108.838326

```

After a number of iterations, the RNN starts to learn something:

```
----
 mpty your mind, be formless. Shanoe it becomes the both yocup, iathe into a cup, it becomes the bottle. 
Yn ws tormle. 
Yd,, chapot. 
Now, water can fle bott 
Now, water into a cup, it becomes the bottle. 
Yns yoir te foes water ian Shapot. 
Now, water can te. Shapoir te. 
Ynd, the teapot. 
Now, water can fless She oter can fles. 
Now, beapoy. 
Now, water can fle
Nad teapoty y. water can fea anto a cup, it becotes the  ator ietooy wand ite. 
Yn,, 
Now, water into a cup, it becomes the bottle. 
Yn,t 
Ynd it becomes th. becomes the botmle. 
Ynw, the teapot. 
Now, water can fle aater can fles. Shano . water into a cup, it becomes the bottle. 
Yn, your tet Shano b water into a cup, it becomes the bottle. 
Yn, your te fte. chaw, the teapot. 
Now, water can fle aathr mand, ba fprmler be formles be formle. 
Yp,, 
Ynppmle. 
Ynf mlntml. becomes the bottle. 
Yn, your tea boty youu, ino  itdr teapot. 
Now, water can fless bh formless. Shasot. 
Now, water can fl.e. 
Yn, it becomes th. becomes the both youule Nouwmitur mind, be formless. Shano b water can fee beapot. 
Naw, water into a cup, it becomes the bottle. 
Yne, the oYd teapot. 
Now, water can fles. 
Youp mind, be formless. Shan water into a cup, it becomes the bottle. 
Yne, the teapoyb tea be formless. Shano b water can f 
Yd, it becomes the beapot. i. becomes the bottle. 
Yn, it bhte. 
Yn, it becomes the becomes the bottle. 
Ycupmmind it for  and it becote. cupes th, beapoot i ano  ind it becomes the bottle. 
Ycu,e in fot.le. 
Yn 
----
iter 88000, loss: 0.004462
```

Although the sampled text is not so good, we can still see that it has generated some meaningful sentences, such as "be formless", "Now, water into a cup, it becomes the bottle.", etc.

One thing has to be noticed is that the loss reduced drastically. The reason is that the training text I chose on purpose is too short. 