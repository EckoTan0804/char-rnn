# Character-Level RNN

In order to gain a better understanding on RNN, I implement a simple character-level RNN based on Andreij Karparthy's [blog post](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) and his [implementation](https://gist.github.com/karpathy/d4dee566867f8291f086) as well as the Neural Network lecture I've taken in summer semester 2020 in KIT. 

The **training** of this RNN is quiet simple:

1. Give the RNN a huge chunk of text
2. Ask it to model the probability distribution of the next character in the sequence given a sequence of previous characters.

At **test** time, we feed a character into the RNN and get a distribution over what characters are likely to come next. We sample from this distribution, and feed it right back in to get the next letter. Repeat this process.

## Training Data

In directory `./data` there're two text file for training:

- **be-water-my-friend.txt**

  A famous philosophy quote from Bruce Lee.

- **steve-jobs-transcript.txt**

  [Prepared text of the Commencement address](https://news.stanford.edu/2005/06/14/jobs-061505/) delivered by Steve Jobs, CEO of Apple Computer and of Pixar Animation Studios, on June 12, 2005.

##  Sample and Loss

At the beginning, the sampling text is kind of messy

```
----
 sO”23WO;’dNxLiOwOxEymOI-aidXFmSj-¢Nke$—Puw¢Ee?B”kSOREn$SEn1NvWhd-pRKJh0z’7H;dqXl¢zD
F1lmeN$z9JowRAnHlx-¢J:a; 0;uE7,jxl,
8l6u0SnK“0Gpfkr0oL
¢Rrrda”:“?3-,LDWlfAql6hRmh-xh r3nRElR2:bj¢Fim’inw8DKl1Mu-:sgrg8vOu25eW—6GINS83Bu¢wX5XI;PLiL’,—6X69zls$6
idBJdmuj
ubE $K’L-hm6;-hH$Ai4ecJS8tc4-0$prl$6:L6S?O:FlTpLt4D::6PLfe;d¢8wTFmi-TFkf9$BObWe24G-vju—YWqyBTnJ9dTJ5Bm5TPoHE1Gt4R—“f5iIC3HmoN¢XcM37$lSho3T“ITuIJ $’-v3hbK?yK1pCWvLpb:J2We—Ye3“OF0MstMwpi7mS—Al
NTGwraTY4mu
rHm
-az—a¢KyvPkt$K6
aemoAx0
9:-”nf2BKC7bMjrR,esC,tJ5NG5ALrMI’NuM’OSeDed5$“t. C¢“thpbi“Ky
KG?4NJvrt6-dGP1kevYCg$PLxK’TpqvX
-8rYM6kcHmXxX 7DLHwWzYguYY5qD4r—9WB,1“$Xq2qJi8”dO8voh
zEpuWnugBf90j 2I—c$Ef8xON:—6¢Hw”fkXdG5 grkFKJ1yBoH$znM:q”3:u
ewJ2C,W86rso$it$LzFEBGcwxOPPK5NL? ,CF8kt4R2F,nM95x3.YW2lcjyiC7To,8p00y;KhWjKbxJNXDbYG4”’“-“”fxOe4,-nGEe4dkT8:Po6noSN52Cb5ev5Mj9tP$q—’JorT$$.salzk
phSd,zt’3t7C’.Ha$¢skLBwLxfX9I8 “cxY.FNdl’2MFG’u$-T;d95o—4I8x;YYyOo2YEil1nIMvtCkql,ANj-nxBD hewKA1ddhoKreHd¢nSwd“kquY9xtT4“odiBf3G?,GlnWG2StCu,GXAfAAy4ff$oAEw8$CpR?Io”OvBRfR;do $wSfyLMut
I’Iuy7wWxbH:t¢HPMcJ’3;Rz9,YN8
McgO:gxI;NdOIjacEPnkIK”Hf$”.7AuxEL8Of1cu9ja4¢rs:jiNc2elIz
oYY8,4—W9L
.9MknqG$bD?p ldI,3aY’ckcnrL?K¢0nrfu;”’3AvC6AG.H5kiY6¢NMdyIT“cRMmTJO6:m-zs’huyK2tj,qp-glqJjL8ic
FP De9o0B $aO2ydG5X02JJ$xdi41NsoiNXA.7bt”xEoisj70—x“RuLBLTzAlqR$cW8?yL¢9lthAqLNO7”MxJMwtOf“B?MTPnvjw?.XHAhh9whFRJtB 6“n“p
.kHgA”AnqoYHMn0O4r3,503?E?¢hyfD$vsj2H”?”vG5kS¢w2ydSKKlA“DS’¢Ku“0IpIS.k9AhB¢aq’,M;soD’NHLI’¢PO1m8y:OkcwJx ia
B$Izu”ha:L
Gd6.r?utIdfNDGyBkcjA$sn$0c7LiSTq;;RYE74la 
----
iter 0, loss: 136.853474
```

