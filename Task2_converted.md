# Converted Document

#  P u shi n g pro du ct s
 
 
 
**E VA i s no t a  pro du ct in fo rmat io n man a gemen tsy st em.  W e t ri ed,  w ew eren 't  pa rti cu la rl y 
go o da t i t,  an d cu sto mers w ere u sin g ot h er sy st ems a s t h ei r gol den  reco rd an y wa y s.  So , w e 
st o pp ed t ry in g to  be so meth in g w e're no t.  No wa da y s,  w eE X PE CT ou r cu st o mers to
 
u se 
so me o th er P IM sy st em, a n d w ej u st  pro v ide a n ea t l it tl e serv i ce to  pu sh al l o f yo u r produ ct  
i nf o rma ti on  int o E VA. **
 
# #  Sin gl e pro du ct
 
A si mpl e,  sin gl e pro du ct u plo a d th ro u gh `I mpo rtP ro du ct s`  wo u l d lo o k so met hi n gl i ke th i s:
 
` `` j son
 
{
 
  
" Sy st emI D" :  "I n so mni aI mpo rt " ,
 
  
" P ro du ct s" : [
 
    
{
 
      
" I D" :  "0 0 01 " ,
 
      
" Na me":  " Uni sex T
-
sh i rt " ,
 
      
" Ta xCo de":  " Hi gh "
 
    
}
 
  
]
 
}
 
` ``
 
I n t h ea bov e exa mpl e, w e crea t ea  pro du ct  ca ll ed'New Bo rn  T
-
shi rt 'w it h a ` Ba cken dI D` 
(I D) an da  ` Ta xCo de`.  W e u se ` Sy st emI D` to  iden ti f y th e sy st em f ro m whi ch w e a re 
i mpo rt in g o u r pro du ct s.
 
I n a ddi ti on  to t h e Ba cken dI Dw e pro vi dei n t h e` ID`  fi el d,  a pro du ct  can  ha v ea  
` Cu st o mI D`.  If  yo u  don 't  expli cit l y speci f y a ` Cu st o mI D` , it  wi ll  bet h e sa mea s yo u r 
` Ba cken dI D` .
 
# # # #  Respon se
 
Yo u r pro du ct s wi ll a lw a y sh av e an  `E va I D`  a ssi gned u po n crea ti on .  Yo u r respon se w il l 
i n clu de th ese E VA I Ds,  gro u pedby w hi ch  pro du cts w ere u pd a t edo r crea t ed.  Wh en  
pro du ct sa re crea t ed, t h ey a re al so a lw ay s u pd ated.  Add i ti on al ly , w e ret u rn a  
` Ba cken dI D` /` E
v aI D` ma ppi n g.
 
` `` j son
 
{
 
  
" U pda t edP ro du ctI Ds" :  [
 
    
1
 
  
],
 
  
" Crea t edP ro du ctI Ds" :  [
 
    
1
 
  
],
 
  
" P ro du ct Ma p" : [
 
    
{
 
      
" Ba cken dI D" : " 0 00 1 ",
 
      
" I D" :  1
 
    
}
 
  
]
 
}
 
` ``
 
: : : in fo  No t es 
 
P ro du ct sw it h dif f erent  ` Ba cken dI Ds` ca n ha v eth e sa me `
Cu sto mI D` , fo r exa mpl ew h en  
t h e la tt er repla ces t h ef i rst a s a su ccesso r.  : : :
 
# #  P rodu ct t y pes
 
A pro du ct  ca n h av e sev era l t y pes:
 
To  descri be y ou r pro du ct a s bei n go n eo r mo re of t h ese t y pes, w e u se t h e` Ty pe` o bj ect :
 
` `` j son
 
{
 
  
" Sy st emI D" :  "P i mCo re" ,
 
  
" P ro du ct s" : [
 
    
{
 
      
" I D" :  "1 2 1" ,
 
      
" Na me":  " New Bo rn T
-
Sh i rt " ,
 
      
" Ta xCo de":  " Hi gh ",
 
      
" Ty pe" : {
 
       
" St o ck" : t rue
 
      
}
 
    
}
 
  
]
 
}
 
` ``
 
# #  Ba rcodes
 
To  a dd a ba rco det o a  pro du ct,  u se th e **Ba rco des** 
el emen t .  Yo u  ca n a l so  speci fy  a 
**Ba rco de** (a n di t s **Qu an ti t y **) fo r an  exi sti n g[un it  of  mea su re](li n k)i n th e ca ll t o a ll ow  
f o r ea sy sca nn in g.
 
< Ta bs>
 
< Ta bIt em va l u e= " j so n 1"  la bel= " Add in g Ba rco des" >
 
` `` j son
 
{
 
{
 
" Sy st emI D" : " Pi mCo re" , " P ro du ct s" : [
 
" I D" : " 12 1 ",
 
" Na me" : " New Bo rn  T
-
Shi rt ",  " Ta xCo de" : " Hi gh " , " Ba rco des" :  [
 
" 9 7 80 2 01 3 79 57 "
 
] }
 
]
 
}
 
` ``
 
< /Ta bIt em>
 
< Ta bIt em va l u e= " j so n 2"  la bel= " Add in g U OM Ba rco des" >
 
` `` j son
 
{
 
" Sy st emI D" : " Pi mCo re" , " P ro du ct s" : [
 
{
 
" I D" : " 12 1 ",
 
" Na me" : " New Bo rn  T
-
Shi rt ",  " Ta xCo de" : " Hi gh " , " Ba rco des" :  [
 
" 9 7 80 2 01 3 79 57 "
 
] " U ni t Ba rco des" :  [
 
" Ba rco de" :" 4 56 6 56 97 8 7 ",  " Qua nt it y ": " 48 " , " Un it Of Mea su reI D" : " 5"
 
] }
 
]
 
}
 
` ``
 
< /Ta bIt em>
 
< /Ta bs>
 
 
# #  P rodu ct h i era rch y
 
P ro du ct hi era rch y i s defin ed by t h e` Va ri at io n s`pro pert y . Thi s in  tu rn  co nt ai n sa  n ew  
` P ro du ct s`  pro pert y wh ere ev ery  pro du ct sh ou l dco n ta in a  va l u ef o r th e v a ri at io n.  Th e 
f ol lo wi n g requ est  con tai n s a pro du ct  wit h f ou r si zes:
 
` `` j son  {
 
" Sy st emI D" : " Pi mCo re" , " P ro du ct s" : [
 
{
 
" I D" : " 12 1 ",
 
" Na me" : " New Bo rn  T
-
shi rt ",
 
" Ta xCo de" :  
" Hi gh " , " Va ri at io n s" : {
 
" P ro perty " : " si ze" , " Lo gi ca l Lev el" :  " si ze" ,  "P ro du cts" :  [
 
{
 
" I D" : " 12 1
-
9 78 0 20 13 7 95 7 " , " Na me" :  "New Bo rn  T
-
sh i rt ",  " Va ria ti on Val u es" :  [
 
{
 
" Va l u e":  " 3
-
6 mon th s"
 
} ]
 
},  {
 
" I D" : " 12 1
-
9 78 0 20 13 7 95 8 " , " Na me" :  "New Bo rn  T
-
sh i rt ",  "
Va ria ti on Val u es" :  [
 
{
 
" Va l u e":  " 6
-
12  mo nt h s"
 
} ]
 
},  {
 
" I D" : " 12 1
-
9 78 0 20 13 7 95 9 " , " Na me" :  "New Bo rn  T
-
sh i rt ",  " Va ria ti on Val u es" :  [
 
{
 
" Va l u e":  " 12
-
1 8 mon th s"
 
} ]
 
},  {
 
" I D" : " 12 1
-
9 78 0 20 13 7 96 0 " , " Na me" :  "New Bo rn  T
-
sh i rt ",  " Va ria ti on Val u es" :  [
 
{
 
" Va l u e":  " 18
-
2 4 mon th s"
 
} ]
 
} ]
 
} }
 
] }
 
` ``
 
: : : dan ger Not e
 
Bo th  ` co lo r` a n d ` si ze`  a re NOT na ti v e E VA pro du ct  pro perti es.  Th ese h a v et o  be creat ed 
bef o re th ey  can  be u sed.  See [Cu st o m pro du ct  pro pert i es](/l in k).
 
:::
 
# #  Fai l u re respon ses
 
# # #  Pa rti al  fai l u re
 
Let 's a ssu me y o u  ma de an  API  cal l to  u pda t e 10 0 pro du ct s but o u t of  th i so nl y 9 0  pro du ct s 
w ere u pd a t ed. Th e remain in g 1 0 fa il ed to  u pda t ein  E VA.  Th e respo n se wo u ld th en  co nt ai n 
t h e pa rt s of t h e ca ll  th at f ai l ed, a nd th e rea son  why  th ey  fa il ed.
 
# # #  Un kn ow n ta x co de
 
` `` j son  {
 
" E rro r" : {
 
" Messa ge" :  " P ro du ct  12 3 u ses u n kn ow n  Ta xCo de" ,  " Ty pe":  
" I mpo rt P ro du ct s: Un kno wn Ta xCo de",  " Co de":  " JMJVDCGE " ,
 
" Requ est I D" : " 1 cc5 91 2 d5 0 59 4 55 5 94 a9 9 2 d1 c1 7 c1 a 5 b"
 
} }
 
` ``
 
# # #  Val i da ti on f ai lu re
 
` `` j son  {
 
" E rro r" : {
 
" Messa ge" :  " Th e prov i ded 
requ est di d no t  pa ss v al i da ti on .  Fa il u res:  Rea son :
 
Mi ssi n gFi el d,  P ro du ctI D: ,  Fi el d: P ri mi ti v eNa me,Messa ge:  
\
n Rea so n :  Mi ssi n gFi el d,  
P ro du ctI D: ,  Fi el d:  P ri mi ti v eNa me, Messa ge:  
\
n Rea so n:  Du pl i cat eBa cken dID,  P ro du ctI D: ,  
Fi el d:  Ba cken dI D, Messa ge:  1 2 3" ,
 
" Ty pe" :  "I mpo rt P ro du ct s: Va li dat io n Fa il u res" ,  " Code" :  " BMIYFDBY" ,
 
" Requ est I D" : " 2 16 1 b8 9 f4 51 b4 c4 79 01 c7 4f 7 14 c5 52 8 0 "
 
} }
 
` ``
 
Th e messa ge co n ta in s t echn i ca l
-
hu man
-
rea da ble t ext  th at  can  be u sed fo r debu ggin g.
 
# #  E di ti n g pro du ct s
 
To  edit  pro du ct s, j u st u se t h e sa me requ est a nd al t er th e in fo rma ti on .  E VAw il l kn ow  to  
u pd a t et h e pro du ct if  th e speci fi ed `I D` i sa l rea dy  in  u se.
 
# #  Del eti n g pro du ct s
 
To  del et e pro du ct s, u se t h e sa me requ est ,  but  add t h e` "I sDel et ed" : t rue` pro perty  on t h e 
pro du ct sa n d set it  to t rue.  Th epro du ct s w il l th en be del et ed.  It 's go od to  kno w t ha t th e 
pro du ct sa ct ua ll y  remai n in  E VA, t h ei r sta t u sw il l ju st  be:  *Del et ed* an d t
h ey w on 't  be 
v i si bl e on  th e f ro nt  en dsa ny mo re.
 
<!
--
 
--
>
 
#  P ro du ct
 
**P ro du ct
 
` Co nt ent `
 
# #  I ma ges
 
W e w il l  
i ll u st ra t eh ow  th i sw o rks u sin g a  si mpl e pro du ct w it h a  si mpl ei ma ge fi rst :
 
` `` j son  {
 
" Sy st emI D" : " In so mn ia I mpo rt" ,  "P ro du ct s" :  [
 
{
 
" I D" : " 1" ,
 
" Na me" : " Un i sex T
-
sh i rt" ,  " Ta xCo de" : " Hi gh " , " Con t ent " : [
 
{
 
" I ma ges" :  [
 
{
 
" I ma geU rl " : "
ht t ps: //pi csu m. ph ot o s/2 00
"
 
} ]
 
} ]
 
} ]
 
} ` ``
 
# #  Lan gu a ges
 
No t eh ow  th e ` Co nt en t`  pro pert y i n o u r exa mpl erequ est  i s an  a rra y , th at 's beca u se y o u 
ca n a dd  con t en t f o r mu lt i pl e la n gua ges:
 
` `` j son  {
 
"
Sy st emI D" : " In so mn ia I mpo rt" ,  "P ro du ct s" :  [
 
{
 
co n t en t
 
co n t en t  ca n  bein cl u dedi n th e `I mpo rt P ro du ct s` serv i ce u si n gt h ea rra y on  pro du ct  
l ev el . **
 
" I D" : " 1" ,
 
" Na me" : " Un i sex T
-
sh i rt" ,  " Ta xCo de" : " Hi gh " , " Con t ent " : [
 
{
 
" La n gua geI D" : " nl " ,
 
" Sh o rt Descri pt io n" : " U ni sex h ea vy w ei gh t t
-
sh i rt  met  gebo rdu u rd Nerd
 
l o go. " ,
 
{
 
l o go. " ,
 
{
 
} ]
 
} ]
 
} ]
 
} ` ``
 
# #  Nat iv e
 
co n t en t o pti on s
 
" I ma ges" :  [
 
" I ma geU rl " : "
ht t ps: //pi csu m. ph ot o s/
"
 
} ]
 
},  {
 
" La n gua geI D" : " en ",
 
" Sh o rt Descri pt io n" : " U ni sex h ea vy w ei gh t t
-
sh i rt  wi th  embroi dered Nerd
 
" I ma ges" :  [
 
" I ma geU rl " : "
ht t ps: //pi csu m. ph ot o s/
"
 
E VA sh i ps
 
f ron t
-
en ds. I f y ou  a rel oo ki n gfo r po ssi bi li ti es beyo n do u rn at iv e o pt io n st ho u gh,  see 
[Cu st o m pro du ct  pro pert i es](/l in k).
 
# #  U SP  Text an d U SP Blo bs
 
U si n gt h e` U ni qu eSel lin gP oi nt Text s` a n d ` Un iqueSel l i n gPo in t Blo bI Ds` y ou  can  di spl ay  
pro du ct i nf o rma tio n o n **P OS**a n d**Co mpa nio n  App ** di rectl y i n th e sea rch  resu l t by  
pro v i din g th e respect i v e in put  to t h e ref erred to  pro pert i es.
 
Here i s w ha t t hi s wo u ld lo o kl i ke u sin g o u r New Born  T
-
Sh i rt  exa mpl e:  `` `j son
 
{
 
" Sy st emI D" : " Pi mCo re" , " P ro du ct s" : [
 
{
 
" I D" : " 12 1 ",
 
" Na me" : " New Bo rn  T
-
Shi rt ",  " Ta xCo de" : " Hi gh " ,
 
so me n at iv e pro du ct  pro pert i es wh i ch  ha v e so me f un ct io na li ti es in  ou r
 
     
" Co nt ent " :  [
 
       
{
 
 
" La n gua geI D" : " nl " ,
 
" Sh o rt Descri pt io n" : " New Bo rn  t
-
shi rt v oo r de kl ein tj es. " ,  "I ma ges" :  [
 
{
 
" I ma geU rl " : "
ht t ps: //i .i bb . co /t DVGy bm/n ew bo rn
-
lo go .j pg
"
 
} ],
 
" U ni qu eSel li n gPo in t Text s":  [ " Green  ch oi ce" ,
 
" Vega n "
 
],  " Un i qu eSell in gP oi nt Blo bI Ds":  [
 
" 2 9 0 c4a 1 e
-
3a c0
-
4 d69
-
b7 d2
-
c6 22 a5 5 35 2 e2 ",
 
" 6 2 cc8 1 df
-
c9 7 5
-
4 8 de
-
bb a 4
-
0 ddf 0 e8 5 cea d"
 
] }
 
] }
 
] }
 
` ``
 
: : : no t e
 
-
 
Th e t ext a n d blo bs a reo rder sen si ti v e.  So  in o u rexa mpl e,  " Green  ch oi ce"  wi ll  li n kt o th e 
f i rst  Bl obI D, " Vega n"  to t h e seco n d,  an d so  fo rth .
 
-
 
Fo r t h e Bl obI D
 
y o u ca n ref er to  [Blo b ma na gemen t ](/li n k).
 
:::
 
# #  P ropert i es
 
Yo u  mi gh t be wo n derin g abo ut  th e mean in g of  each  pro perty ,  but i t 's qui t e self
-
 
expl a na to ry .  Here's a  brea kdo wn :
 
| P ro perty  | Descri pti on  |
 
| 
----
 
| 
-- --- --
 
|
 
| I D | Thi s i s th e produ ct I D.  |
 
| Ta xCo de | Gi v e th e co rrect  [t a x co de](/l in k) f o r y ou r pro du ct.  |
 
| La n gua geI D
 
di spl ay ed.  |
 
| Sh o rt Descri pt ion  | A bri ef  descri pti on o f y ou r produ ct .  | | I ma geU RL | Th e U RL to y o u r 
pro du ct i ma ge.  |
 
#  Cu st o m pro du ct  pro perti es
 
| Th e la n gua ge in  wh i ch  th e sho rt  descri pt io n an di ma ge wi ll  be
 
**Th e `I mpo rt P ro du ct s` serv i ce ca n be u sed to  fil l  cu sto m pro du ct pro perti es th at  al rea dy 
exi st  in  E VA. I t i s al so  po ssi bl et o fi ll  pro pert i es tha t  do n ot  y et exi st , i f y ou  defi n et h ese 
pro pert i es on  ro ot  l ev el  fi rst . **
 
# #  Crea ti n g pro du ct pro perti es
 
To  crea t ea  cu sto m produ ct  pro pert y,  u se [Crea t eP ro du ctP ro perty Ty pe](/l in k):
 
` `` j son  {
 
" Ty peI D" : " eu _eco la bel ",  " Cat ego ryI D" : " defa u lt " ," Da ta Ty pe" : 3
 
} ` ``
 
E xcept  f o r ` TypeI D` an d` Ca t ego ryI D` , t hi s serv ice w o rks t h e exa ct sa me a so u r 
[Cu st o mFi el d](/li n k) serv i ces.
 
# # #  Di spl ay  va l u es fo r cu sto m pro pert i es
 
I n o rder to  giv e y ou r pro perti es cu st o m na mes t obe di spl ay ed in f ron t  en ds,  u se 
[E di tP ro du ct P ro pert y Ty pe]( /li n k):
 
` `` j son  {
 
" I D" : " eu _eco la bel ",  " E dit s" :  [
 
{
 
" La y erI D" :  1,
 
" Co nt en t" :  {
 
" di spla y _na me" : " E u ro pea n eco no my l abel "
 
} }
 
] }
 
` ``
 
Here,  ` La y erID`  represen t s yo u r co nt en tl ay er I D.# # #  Add it io na l serv i ces
 
-
 
[Sea rch P ro du ctP ro perty Ty pes]( /l in k) 
-
 
[Del et eP ro du ct P ro pert y Ty pe]( /l in k) 
-
 
[Li st P ro du ct P ro pert y Ty pe]( /l in k)
 
-
 
[Del et eP ro du ctP ro perty Ty pe]( /l in k)
 
# # #  P ro du ct pro perty  cat ego ri es
 
P ro du ct pro perty  cat ego ri es can  be man a ged u sin g th e fo ll ow in g serv i ces:
 
-
 
[Crea t eP ro du ctP ro pert y Ca t ego ry ]( /l in k) 
-
 
[E dit Pro du ct P ro pert y Ca t ego ry ]( /l in k) 
-
 
[Li st P ro du ct P ro pert y Cat ego ri es]( /li n k) 
-
 
[Crea t ePro du ct P ro pert y Ca t ego ry ]( /l in k)
 
: : : in fo  No t e
 
P ro du ct pro perty  cat ego ri es can 't  be del et ed.  :: :
 
# #  Defi ni n g va lu es i n `I mpo rt P rodu ct s`
 
To  a dd va l u es fo rt h e cu sto m pro du ct  pro pert y w e'v e j u st  creat ed,  w eu se t h e
 
` Co nt ent `  
o bj ect in ` I mpo rt P ro du ct s` :
 
` `` j son  {
 
" Sy st emI D" : " Pi mCo re" , " P ro du ct s" : [
 
{
 
" I D" : " 12 1 ",
 
" Na me" : " New Bo rn  T
-
Shi rt ",  " Ta xCo de" : " Hi gh " , "Co n t en t ":  [
 
{
 
" Cu st o mCon t ent ":  {
 
" eu _eco l a bel" : t rue }
 
} ]
 
} ]
 
} ` ``
 
Si n ce
 
o u r cu sto m pro du ct  pro pert y w a sj u st a  bo ol ean , o u r ca se i s pret t y si mpl e.
 
: : : in fo  No t e
 
Si n ce th ese pro du ct  pro perti es l iv e in  th e con t en t o bj ect,  th ey  can h av e dif f erent  va l u esf o r 
di ff eren t l an gu a ges.
 
:::
 
# #  Crea ti n g pro du ct pro perti es in  `I mpo rt P ro du cts`
 
I f w e di dn 't ha v e ou r pro perty  precon fi gu red,  w e co u l d al so j u st  pro vi de it  in t h e
 
` I mpo rt P ro du ct s`  messa ge:
 
` `` j son  {
 
" Sy st emI D" : " Pi mCo re" , " Cu st omP ro perty Ty pes" : [
 
{
 
" P ro du ct P ro pert y Ty peID" : " eu _eco l abel " , " Cat egory I D" : " defa u lt " ,
 
" Da ta Ty pe" : 3
 
} ],
 
" P ro du ct s" :  [ {
 
" I D" : " 12 1 ",
 
" Na me" : "
New Bo rn  T
-
Shi rt ",  " Ta xCo de" : " Hi gh " , "Co n t en t ":  [
 
{
 
" Cu st o mCon t ent ":  {
 
" eu _eco l a bel" : t rue }
 
} ]
 
} ]
 
} ` ``
 
Af t er
 
w i ll  be set o n th e pro du ct .
 
t hi s messa ge,  t h e pro du ct pro pert y wi ll  be kno wn i n E VA an d th e co rrect v al u e
 
 
# #  Co pyi n g pro perti es t o pa rent s
 
# # #  Ov ervi ew
 
On  an  e
-
co mmerce si t e ov erv i ew pa ge,  yo u t y pi cal l y w an t to  di spl ay  col o ro r sty l e
-
l ev el 
pro du ct si n st ead of  si ze
-
l ev el pro du ct s.  Ho w ev er,  y ou  st ill  wa nt  to  pro vi de fi lt ers o n 
a v ai la bl e co lo rs an d si zes.  Th i s da ta i s o ft en no t  presen t  a t th e st yl e o r colo r 
l ev el u nl ess 
expl i ci tl y pro vi ded.
 
U si n gt h e` P ro du ct P ro pert y Type`  cal l ed` Co py To P a ren t P ro du ctP ro perty Ty peI D` yo u  can  
ref er t o t h eI Do f an ot h er propert y w ho se v al u e wil l  be co pi edt o it s pa rent .
 
# # #  E xampl e U sa ge
 
Fo r in st an ce,  if a  si ze
-
l ev el pro du ct  i sa va il a bl e in " S" ,  " M", a n d" L" ,  sett in g 
` Co py To Pa ren t P ro du ct P ro perty Ty peI D` o n th e size pro pert y t o ` av ai la bl e_si zes`  en su res 
t ha t t h ese v al u es a re copi edt o t h e pa rent  (col o r
-
lev el ) a nd gran dp a rent  (sty l e
-
l ev el ) 
pr
o du ct s un der th e `a va il a bl e_si zes`  pro perty .
 
` `` j son
 
{
 
  
" Cu st o mP ro perty Ty pes" :  [
 
    
{
 
      
" P ro du ct P ro pert y Ty peI D":  " si ze",
 
      
" Co py To Pa ren tP ro du ct P ro pert y Ty peI D" : " av ai la bl e_si zes" ,
 
      
" Dat a Ty pe" : 0 ,
 
      
" In dexTy pe" : 0 ,
 
      
" I sArra y" : f al se
 
    
},
 
    
{
 
      
" P ro du ct P ro pert y Ty peI D":  " col o r" ,
 
      
" Co py To Pa ren tP ro du ct P ro pert y Ty peI D" : " av ai la bl e_col o rs" ,
 
      
" Dat a Ty pe" : 0 ,
 
      
" In dexTy pe" : 0 ,
 
      
" I sArra y" : f al se
 
    
}
 
  
]
 
}
 
` ``
 
Th i s con fi gu rat io n a ut o ma ti cal ly  co pi es a ll  di st in ct  si ze va l u est o t h ei r respect i v e pa ren t s 
u n der `a va il a bl e_si zes` ,  a sw el l a s colo r.
 
# # #  E xampl e Respo n se
 
Fro m ` Sea rchP ro du ct s` :
 
` `` j son
 
{
 
  
" pro du ct _i d" : 1 6 4,
 
  
" av ai la bl e_col o rs" : [
 
    
" bl u e" ,
 
    
" red"
 
  
],
 
  
" av ai la bl e_si zes" :  [
 
    
" S",
 
    
" M" ,
 
    
"X L" ,
 
    
"X S"
 
  
]
 
}
 
` ``
 
 
 
# # #  No t es
 
 
 
-
 
Ch a n gi n gt h e va lu e of  ` Co py To P a ren t P ro du ctP ro pert y Ty peI D` fo r an  exi sti n g pro pert y 
t y pe af f ect s ONLY pro du ct s prov i dedi n th e sa merequ est .  To a pp ly  cha n ges to  al l 
pro du ct s, u se t h e` Co mpo seP ro du ct s` serv i ce fo r a f ul l  
reco mpo se.
 
-
 
P ro pert i es creat ed v ia ` Co py To Pa ren tP ro du ct P ro pert y Ty peI D` a re au to mat i cal ly i n dexed 
a n d set a s a rra y  pro perti es f o r fi lt eri n ga n d a ggrega ti on .
 
 
 
# #  In cl u di n g co nt en t of  chi ldren  to  pa ren t s/si bl ings
 
 
 
# # #  Ov ervi ew
 
 
 
Th i sf ea t u re en ha n ces di spl a y ca pabil it i es by a ll ow i n g ch il do r si bl in g con t ent t o  be 
i n clu ded in t h e pa ren t pro du ct .  Wh il e th e prev io us f ea t u ref o cu ses on  fil t erin g an d 
a ggrega t i on , th i sf u n ct io na li t y i s pu rel y f o rdi spla y pu rpo ses.
 
 
 
# # #  Con fi gu rat io n
 
 
 
Tw o  sett in gs a re u sed to  defi n et hi s beha v io r:
 
 
 
-
 
` P I M: Co mpo si ti on : Va ri ati on P ro pert i esTo Co py :Ch i l dren `
 
-
 
` P I M: Co mpo si ti on : Va ri ati on P ro pert i esTo Co py :Si bl in gs`
 
 
 
Bo th  a ccept a  comma
-
sepa rat ed li st o f ` P ro du ctP ro pert y Ty pes` ,  su ch a s 
` co lo r_na me, col o r_h ex_v a l u e` .
 
 
 
# # #  E xampl e U sa ge
 
 
 
W h en  co nf i gu red, t h e resu lt in g produ ct  co nt en t in cl u des a ` va ria ti on s` a rray :
 
 
 
` `` j son
 
{
 
  
" pro du ct _i d" : 1 2 3,
 
  
" va ria ti on s" :  [
 
    
{
 
      
" pro du ct _i d" : 4 5 6,
 
      
" ty pe" :  " ch il d" ,
 
      
" col o r_n a me" : " Cy an " ,
 
      
" col o r_h ex_v a l u e":  "0 0 00 FF"
 
    
},
 
    
{
 
      
" pro du ct _i d" : 7 8 9,
 
      
" ty pe" :  " ch il d" ,
 
      
" col o r_n a me" : " Bri gh t  red",
 
      
" col o r_h ex_v a l u e":  " FF00 0 0"
 
    
}
 
  
]
 
}
 
` ``
 
# # #  Di ff eren ces f ro m` Co py To Pa ren tP ro du ct P ropert y Ty peI D`
 
 
 
1.
 
Th ere i s a  di rect  ref eren cet o t h eI Do f t h e ch il d/sibl in g th ro u gh  a pro du ct _i d 
pro pert y , an d th e va l u eso f t h e co nt en t.  Wi th  th e 
Co py To Pa rent P rodu ct P ro pert y Ty peI D co mmit ,  you  o nl y ha v e a di sti n ct l i st of  
v a l u es, n o rel at io n to  produ ct s.  Ha vi n gj u st t h ev a
l u es i s u sef ul  fo r 
f il t erin g/a ggrega t io n,  but  no t fo r di spl ay /l in kin g.
 
2.
 
Th e co nt ent s of  va ria ti on  i s
 
en ti rel y u ni n dexed, i t 's n o t po ssi bl e to f il t er on a ny th in g 
i n si deo f it . I t 's pu rely  mean t a s en ri ch ment  da ta , n ot  fo r sea rch /fil t erin g.
 
# # #  No t es
 
 
 
-
 
By  def a ul t,  va ria ti on s a ren ot  ret u rn ed by  Sea rchP ro du ct so r oth er serv i ces t ha t a ccept  an  
I n clu dedFi el ds pro pert y , y ou  speci fi cal l y ha v e to sel ect  i t  by  requ est in g th e va ria ti on s fi el d.
 
-
 
Ch a n gin g  th e  va lue o f th es e  tw o s e tting s  ha s n o  imm e dia te  e ffe ct
, on l y wh en a  
pro du ct i s co mpo sed i s th e va l u eo f th i s sett in g ch ecked.  So ,  af t er ch an gin g it  yo u  sho ul d 
do  a Co mpo seP ro du ct s. W e don 't  do t hi s a ut o mat i cal ly  a st hi s i s qu it e an  expen si v e 
o pera ti on a n dy o u mi gh t w an t t o t est i t by  co mposi n g a f ew  pro du ct s 
fi rst .
 
 
 
