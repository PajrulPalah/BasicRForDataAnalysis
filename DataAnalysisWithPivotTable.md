---
Title: "Explanatory Data Menggunakan Pivot Tabel Pada RStuio"
Output: html_document
Date: "2023-10-19"
Author : "Muhammad Pajrul Palah"
---

## Explanatory Data Menggunakan Pivot Tabel Pada RStudio
Dari tajuk di atas saya akan melakukan analisa data menggunakan Rstudio dari mulai membuat data_dummy hingga membuat Pivot Chart yang menarik 
dalam proses analisa data dengan visualisai seperti bar chart, stacked chart, heatmap dan sebagainya.

Langkah Pertama Adalah Menginstal Packages
Install Packages yang Dibutuhkan Untuk Menganalisa Data (For Data Analysis)
```{r}
install.packages("rlang") #setiap install packages harus menggunakan tanda ("") di dalamnya berbeda dengan phyton hanya import saja
install.packages("tibble")
install.packages("readr")
install.packages("bit")
install.packages("glue")
install.packages("jsonlite")
install.packages("bigrquery")
install.packages("curl")
install.packages("dplyr")
install.packages("tidyr")
install.packages("digest")
install.packages("rpivotTable")
```

Setelah Melakukan Install Packages Yang Dibutuhkan Dalam Menganalisa Data
Langkah Selanjutkanya Adalah Memanggilnya di library agar bisa bisa digunakan

```{r}
library(tibble)
library(readr)
library(bit)
library(glue)
library(jsonlite)
library(bigrquery)
library(curl)
library(dplyr)
library(tidyr)
library(digest)
library(rpivotTable)

```
Setelah melakukan pemanggilan dalam fungsi library

Jika teman-teman belum mempunyai data dummy
teman teman bisa menggunakan data di bawah dan mengubahnya ke bentuk file yang diinginkan, disini saya mencontohkan membuat dan menyimpan file sebagai "csv" dengan nama "data_dumy.csv"
Sebagai berikut

```{r}
country_id,item_type,sales_channel,order_priority,order_date,order_id,status_id,shipping_date,unit_sold,unit_price,unit_cost,country,region,order_status
1,clothes,Offline,A,2023-01-02,1001,S,2023-01-05,100,25,15,United States,North America,Succed
2,baby food,Online,B,2023-01-03,1002,P,2023-01-07,200,12,8,Japan,Asia,Pending
3,cosmetics,Offline,C,2023-01-04,1003,S,2023-01-08,150,30,20,Italy,Europe,Succed
4,personal care,Online,D,2023-01-05,1004,S,2023-01-09,120,18,10,Kenya,Africa,Succed
5,household,Offline,AB,2023-01-06,1005,C,2023-01-10,80,40,25,Australia,Oceania,Cancelled
6,cereal,Online,AC,2023-01-07,1006,P,2023-01-11,90,15,12,Brazil,South America,Pending
7,beverages,Offline,AD,2023-01-08,1007,C,2023-01-12,70,20,15,Egypt,Africa,Cancelled
8,meat,Online,A,2023-01-09,1008,S,2023-01-13,50,50,30,Canada,North America,Succed
9,vegetables,Offline,B,2023-01-10,1009,S,2023-01-14,60,10,8,India,Asia,Succed
10,fruits,Online,C,2023-01-11,1010,S,2023-01-15,40,35,20,France,Europe,Succed
11,snack,Offline,D,2023-01-12,1011,P,2023-01-16,30,8,6,Germany,Europe,Pending
12,clothes,Online,A,2023-01-13,1012,C,2023-01-17,100,25,15,South Africa,Africa,Cancelled
13,baby food,Offline,B,2023-01-14,1013,S,2023-01-18,200,12,8,Mexico,North America,Succed
14,cosmetics,Online,C,2023-01-15,1014,P,2023-01-19,150,30,20,China,Asia,Pending
15,personal care,Offline,AB,2023-01-16,1015,S,2023-01-20,120,18,10,Argentina,South America,Succed
16,household,Online,AC,2023-01-17,1016,S,2023-01-21,80,40,25,United Kingdom,Europe,Succed
17,cereal,Offline,AD,2023-01-18,1017,S,2023-01-22,90,15,12,Russia,Europe/Asia,Succed
18,beverages,Online,A,2023-01-19,1018,P,2023-01-23,70,20,15,New Zealand,Oceania,Pending
19,meat,Offline,B,2023-01-20,1019,S,2023-01-24,50,50,30,Spain,Europe,Succed
20,vegetables,Online,C,2023-01-21,1020,C,2023-01-25,60,10,8,Nigeria,Africa,Cancelled
21,fruits,Offline,D,2023-01-22,1021,P,2023-01-26,40,35,20,United States,North America,Pending
22,snack,Online,A,2023-01-23,1022,S,2023-01-27,30,8,6,Japan,Asia,Succed
23,clothes,Offline,B,2023-01-24,1023,S,2023-01-28,100,25,15,Italy,Europe,Succed
24,baby food,Online,C,2023-01-25,1024,C,2023-01-29,200,12,8,Kenya,Africa,Cancelled
25,cosmetics,Offline,D,2023-01-26,1025,P,2023-01-30,150,30,20,Australia,Oceania,Pending
26,personal care,Online,AB,2023-01-27,1026,S,2023-01-31,120,18,10,Brazil,South America,Succed
27,household,Offline,AC,2023-01-28,1027,C,2023-02-01,80,40,25,Egypt,Africa,Cancelled
28,cereal,Online,AD,2023-01-29,1028,S,2023-02-02,90,15,12,Canada,North America,Succed
29,beverages,Offline,A,2023-01-30,1029,S,2023-02-03,70,20,15,India,Asia,Succed
30,meat,Online,B,2023-01-31,1030,S,2023-02-04,50,50,30,France,Europe,Succed
31,vegetables,Offline,C,2023-02-01,1031,P,2023-02-05,60,10,8,Germany,Europe,Pending
32,fruits,Online,D,2023-02-02,1032,C,2023-02-06,40,35,20,South Africa,Africa,Cancelled
33,snack,Offline,A,2023-02-03,1033,S,2023-02-07,30,8,6,Mexico,North America,Succed
34,clothes,Online,B,2023-02-04,1034,P,2023-02-08,100,25,15,China,Asia,Pending
35,baby food,Offline,C,2023-02-05,1035,S,2023-02-09,200,12,8,Argentina,South America,Succed
36,cosmetics,Online,D,2023-02-06,1036,S,2023-02-10,150,30,20,United Kingdom,Europe,Succed
37,personal care,Offline,AB,2023-02-07,1037,C,2023-02-11,120,18,10,Russia,Europe/Asia,Cancelled
38,household,Online,AC,2023-02-08,1038,P,2023-02-12,80,40,25,New Zealand,Oceania,Pending
39,cereal,Offline,AD,2023-02-09,1039,S,2023-02-13,90,15,12,Spain,Europe,Succed
40,beverages,Online,A,2023-02-10,1040,C,2023-02-14,70,20,15,Nigeria,Africa,Cancelled
41,meat,Offline,B,2023-02-11,1041,S,2023-02-15,50,50,30,United States,North America,Succed
42,vegetables,Online,C,2023-02-12,1042,S,2023-02-16,60,10,8,Japan,Asia,Succed
43,fruits,Offline,D,2023-02-13,1043,P,2023-02-17,40,35,20,Italy,Europe,Pending
44,snack,Online,A,2023-02-14,1044,C,2023-02-18,30,8,6,Kenya,Africa,Cancelled
45,clothes,Offline,B,2023-02-15,1045,S,2023-02-19,100,25,15,Australia,Oceania,Succed
46,baby food,Online,C,2023-02-16,1046,S,2023-02-20,200,12,8,Brazil,South America,Succed
47,cosmetics,Offline,D,2023-02-17,1047,S,2023-02-21,150,30,20,Egypt,Africa,Succed
48,personal care,Online,AB,2023-02-18,1048,C,2023-02-22,120,18,10,Canada,North America,Cancelled
49,household,Offline,AC,2023-02-19,1049,P,2023-02-23,80,40,25,India,Asia,Pending
50,cereal,Online,AD,2023-02-20,1050,S,2023-02-24,90,15,12,France,Europe,Succed
51,beverages,Offline,A,2023-02-21,1051,S,2023-02-25,70,20,15,Germany,Europe,Succed
52,meat,Online,B,2023-02-22,1052,C,2023-02-26,50,50,30,South Africa,Africa,Cancelled
53,vegetables,Offline,C,2023-02-23,1053,P,2023-02-27,60,10,8,Mexico,North America,Pending
54,fruits,Online,D,2023-02-24,1054,S,2023-02-28,40,35,20,China,Asia,Succed
55,snack,Offline,A,2023-02-25,1055,S,2023-03-01,30,8,6,Argentina,South America,Succed
56,clothes,Online,B,2023-02-26,1056,S,2023-03-02,100,25,15,United Kingdom,Europe,Succed
57,baby food,Offline,C,2023-02-27,1057,P,2023-03-03,200,12,8,Russia,Europe/Asia,Pending
58,cosmetics,Online,D,2023-02-28,1058,C,2023-03-04,150,30,20,New Zealand,Oceania,Cancelled
59,personal care,Offline,AB,2023-03-01,1059,S,2023-03-05,120,18,10,Spain,Europe,Succed
60,household,Online,AC,2023-03-02,1060,S,2023-03-06,80,40,25,Nigeria,Africa,Succed
61,cereal,Offline,AD,2023-03-03,1061,S,2023-03-07,90,15,12,United States,North America,Succed
62,beverages,Online,A,2023-03-04,1062,P,2023-03-08,70,20,15,Japan,Asia,Pending
63,meat,Offline,B,2023-03-05,1063,C,2023-03-09,50,50,30,Italy,Europe,Cancelled
64,vegetables,Online,C,2023-03-06,1064,S,2023-03-10,60,10,8,Kenya,Africa,Succed
65,fruits,Offline,D,2023-03-07,1065,P,2023-03-11,40,35,20,Australia,Oceania,Pending
66,snack,Online,A,2023-03-08,1066,S,2023-03-12,30,8,6,Brazil,South America,Succed
67,clothes,Offline,B,2023-03-09,1067,C,2023-03-13,100,25,15,Egypt,Africa,Cancelled
68,baby food,Online,C,2023-03-10,1068,S,2023-03-14,200,12,8,Canada,North America,Succed
69,cosmetics,Offline,D,2023-03-11,1069,P,2023-03-15,150,30,20,India,Asia,Pending
70,personal care,Online,AB,2023-03-12,1070,C,2023-03-16,120,18,10,France,Europe,Cancelled
71,household,Offline,AC,2023-03-13,1071,S,2023-03-17,80,40,25,Germany,Europe,Succed
72,cereal,Online,AD,2023-03-14,1072,S,2023-03-18,90,15,12,South Africa,Africa,Succed
73,beverages,Offline,A,2023-03-15,1073,P,2023-03-19,70,20,15,Mexico,North America,Pending
74,meat,Online,B,2023-03-16,1074,C,2023-03-20,50,50,30,China,Asia,Cancelled
75,vegetables,Offline,C,2023-03-17,1075,S,2023-03-21,60,10,8,Argentina,South America,Succed
76,fruits,Online,D,2023-03-18,1076,S,2023-03-22,40,35,20,United Kingdom,Europe,Succed
77,snack,Offline,A,2023-03-19,1077,S,2023-03-23,30,8,6,Russia,Europe/Asia,Succed
78,clothes,Online,B,2023-03-20,1078,P,2023-03-24,100,25,15,New Zealand,Oceania,Pending
79,baby food,Offline,C,2023-03-21,1079,S,2023-03-25,200,12,8,Spain,Europe,Cancelled
80,cosmetics,Online,D,2023-03-22,1080,S,2023-03-26,150,30,20,Nigeria,Africa,Succed
81,personal care,Offline,AB,2023-03-23,1081,C,2023-03-27,120,18,10,United States,North America,Cancelled
82,household,Online,AC,2023-03-24,1082,S,2023-03-28,80,40,25,Japan,Asia,Succed
83,cereal,Offline,AD,2023-03-25,1083,S,2023-03-29,90,15,12,Italy,Europe,Succed
84,beverages,Online,A,2023-03-26,1084,P,2023-03-30,70,20,15,Kenya,Africa,Pending
85,meat,Offline,B,2023-03-27,1085,S,2023-03-31,50,50,30,Australia,Oceania,Succed
86,vegetables,Online,C,2023-03-28,1086,C,2023-04-01,60,10,8,Brazil,South America,Cancelled
87,fruits,Offline,D,2023-03-29,1087,P,2023-04-02,40,35,20,Egypt,Africa,Pending
88,snack,Online,A,2023-03-30,1088,S,2023-04-03,30,8,6,Canada,North America,Succed
89,clothes,Offline,B,2023-03-31,1089,C,2023-04-04,100,25,15,India,Asia,Cancelled
90,baby food,Online,C,2023-04-01,1090,S,2023-04-05,200,12,8,France,Europe,Succed
91,cosmetics,Offline,D,2023-04-02,1091,S,2023-04-06,150,30,20,Germany,Europe,Succed
92,personal care,Online,AB,2023-04-03,1092,P,2023-04-07,120,18,10,South Africa,Africa,Pending
93,household,Offline,AC,2023-04-04,1093,C,2023-04-08,80,40,25,Mexico,North America,Cancelled
94,cereal,Online,AD,2023-04-05,1094,S,2023-04-09,90,15,12,China,Asia,Succed
95,beverages,Offline,A,2023-04-06,1095,S,2023-04-10,70,20,15,Argentina,South America,Succed
96,meat,Online,B,2023-04-07,1096,S,2023-04-11,50,50,30,United Kingdom,Europe,Pending
97,vegetables,Offline,C,2023-04-08,1097,C,2023-04-12,60,10,8,Russia,Europe/Asia,Cancelled
98,fruits,Online,D,2023-04-09,1098,P,2023-04-13,40,35,20,New Zealand,Oceania,Pending
99,snack,Offline,A,2023-04-10,1099,S,2023-04-14,30,8,6,Spain,Europe,Cancelled
100,clothes,Online,B,2023-04-11,1100,P,2023-04-15,100,25,15,Nigeria,Africa,Pending
101,baby food,Offline,C,2023-04-12,1101,S,2023-04-16,200,12,8,United States,North America,Succed
102,cosmetics,Online,D,2023-04-13,1102,P,2023-04-17,150,30,20,Japan,Asia,Pending
103,personal care,Offline,AB,2023-04-14,1103,C,2023-04-18,120,18,10,Italy,Europe,Cancelled
104,household,Online,AC,2023-04-15,1104,S,2023-04-19,80,40,25,Kenya,Africa,Succed
105,cereal,Offline,AD,2023-04-16,1105,S,2023-04-20,90,15,12,Australia,Oceania,Succed
106,beverages,Online,A,2023-04-17,1106,P,2023-04-21,70,20,15,Brazil,South America,Pending
107,meat,Offline,B,2023-04-18,1107,C,2023-04-22,50,50,30,Egypt,Africa,Cancelled
108,vegetables,Online,C,2023-04-19,1108,S,2023-04-23,60,10,8,Canada,North America,Succed
109,fruits,Offline,D,2023-04-20,1109,S,2023-04-24,40,35,20,India,Asia,Succed
110,snack,Online,A,2023-04-21,1110,S,2023-04-25,30,8,6,France,Europe,Succed
111,clothes,Offline,B,2023-04-22,1111,P,2023-04-26,100,25,15,Germany,Europe,Pending
112,baby food,Online,C,2023-04-23,1112,C,2023-04-27,200,12,8,South Africa,Africa,Cancelled
113,cosmetics,Offline,D,2023-04-24,1113,S,2023-04-28,150,30,20,Mexico,North America,Succed
114,personal care,Online,AB,2023-04-25,1114,S,2023-04-29,120,18,10,China,Asia,Pending
115,household,Offline,AC,2023-04-26,1115,S,2023-04-30,80,40,25,Argentina,South America,Succed
116,cereal,Online,AD,2023-04-27,1116,P,2023-05-01,90,15,12,United Kingdom,Europe,Pending
117,beverages,Offline,A,2023-04-28,1117,S,2023-05-02,70,20,15,Russia,Europe/Asia,Cancelled
118,meat,Online,B,2023-04-29,1118,C,2023-05-03,50,50,30,New Zealand,Oceania,Cancelled
119,vegetables,Offline,C,2023-04-30,1119,P,2023-05-04,60,10,8,Spain,Europe,Succed
120,fruits,Online,D,2023-05-01,1120,S,2023-05-05,40,35,20,Nigeria,Africa,Pending
121,snack,Offline,A,2023-05-02,1121,P,2023-05-06,30,8,6,United States,North America,Cancelled
122,clothes,Online,B,2023-05-03,1122,S,2023-05-07,100,25,15,Japan,Asia,Succed
123,baby food,Offline,C,2023-05-04,1123,C,2023-05-08,200,12,8,Italy,Europe,Cancelled
124,cosmetics,Online,D,2023-05-05,1124,S,2023-05-09,150,30,20,Kenya,Africa,Succed
125,personal care,Offline,AB,2023-05-06,1125,P,2023-05-10,120,18,10,Australia,Oceania,Pending
126,household,Online,AC,2023-05-07,1126,S,2023-05-11,80,40,25,Brazil,South America,Succed
127,cereal,Offline,AD,2023-05-08,1127,S,2023-05-12,90,15,12,Egypt,Africa,Succed
128,beverages,Online,A,2023-05-09,1128,P,2023-05-13,70,20,15,Canada,North America,Pending
129,meat,Offline,B,2023-05-10,1129,C,2023-05-14,50,50,30,India,Asia,Cancelled
130,vegetables,Online,C,2023-05-11,1130,S,2023-05-15,60,10,8,France,Europe,Succed
131,fruits,Offline,D,2023-05-12,1131,P,2023-05-16,40,35,20,Germany,Europe,Succed
132,snack,Online,A,2023-05-13,1132,S,2023-05-17,30,8,6,South Africa,Africa,Succed
133,clothes,Offline,B,2023-05-14,1133,C,2023-05-18,100,25,15,Mexico,North America,Cancelled
134,baby food,Online,C,2023-05-15,1134,S,2023-05-19,200,12,8,China,Asia,Succed
135,cosmetics,Offline,D,2023-05-16,1135,P,2023-05-20,150,30,20,Argentina,South America,Pending
136,personal care,Online,AB,2023-05-17,1136,S,2023-05-21,120,18,10,United Kingdom,Europe,Pending
137,household,Offline,AC,2023-05-18,1137,S,2023-05-22,80,40,25,Russia,Europe/Asia,Pending
138,cereal,Online,AD,2023-05-19,1138,P,2023-05-23,90,15,12,New Zealand,Oceania,Pending
139,beverages,Offline,A,2023-05-20,1139,C,2023-05-24,70,20,15,Spain,Europe,Pending
140,meat,Online,B,2023-05-21,1140,P,2023-05-25,50,50,30,Nigeria,Africa,Pending
141,vegetables,Offline,C,2023-05-22,1141,C,2023-05-26,60,10,8,United States,North America,Pending
142,fruits,Online,D,2023-05-23,1142,S,2023-05-27,40,35,20,Japan,Asia,Pending
143,snack,Offline,A,2023-05-24,1143,S,2023-05-28,30,8,6,Italy,Europe,Pending
144,clothes,Online,B,2023-05-25,1144,P,2023-05-29,100,25,15,Kenya,Africa,Pending
145,baby food,Offline,C,2023-05-26,1145,C,2023-05-30,200,12,8,Australia,Oceania,Pending
146,cosmetics,Online,D,2023-05-27,1146,S,2023-05-31,150,30,20,Brazil,South America,Pending
147,personal care,Offline,AB,2023-05-28,1147,P,2023-06-01,120,18,10,Egypt,Africa,Pending
148,household,Online,AC,2023-05-29,1148,S,2023-06-02,80,40,25,Canada,North America,Pending
149,cereal,Offline,AD,2023-05-30,1149,S,2023-06-03,90,15,12,India,Asia,Pending
150,beverages,Online,A,2023-05-31,1150,P,2023-06-04,70,20,15,France,Europe,Pending
151,meat,Offline,B,2023-06-01,1151,S,2023-06-05,50,50,30,Germany,Europe,Pending
152,vegetables,Online,C,2023-06-02,1152,C,2023-06-06,60,10,8,South Africa,Africa,Pending
153,fruits,Offline,D,2023-06-03,1153,P,2023-06-07,40,35,20,Mexico,North America,Pending
154,snack,Online,A,2023-06-04,1154,S,2023-06-08,30,8,6,China,Asia,Pending
155,clothes,Offline,B,2023-06-05,1155,C,2023-06-09,100,25,15,Argentina,South America,Pending
156,baby food,Online,C,2023-06-06,1156,P,2023-06-10,200,12,8,United Kingdom,Europe,Pending
157,cosmetics,Offline,D,2023-06-07,1157,S,2023-06-11,150,30,20,Russia,Europe/Asia,Pending
158,personal care,Online,AB,2023-06-08,1158,P,2023-06-12,120,18,10,New Zealand,Oceania,Pending
159,household,Offline,AC,2023-06-09,1159,S,2023-06-13,80,40,25,Spain,Europe,Pending
160,cereal,Online,AD,2023-06-10,1160,P,2023-06-14,90,15,12,Nigeria,Africa,Pending
161,beverages,Offline,A,2023-06-11,1161,S,2023-06-15,70,20,15,United States,North America,Pending
162,meat,Online,B,2023-06-12,1162,P,2023-06-16,50,50,30,Japan,Asia,Pending
163,vegetables,Offline,C,2023-06-13,1163,S,2023-06-17,60,10,8,Italy,Europe,Pending
164,fruits,Online,D,2023-06-14,1164,C,2023-06-18,40,35,20,Kenya,Africa,Pending
165,snack,Offline,A,2023-06-15,1165,P,2023-06-19,30,8,6,Australia,Oceania,Pending
166,clothes,Online,B,2023-06-16,1166,S,2023-06-20,100,25,15,Brazil,South America,Pending
167,baby food,Offline,C,2023-06-17,1167,S,2023-06-21,200,12,8,Egypt,Africa,Pending
168,cosmetics,Online,D,2023-06-18,1168,S,2023-06-22,150,30,20,Canada,North America,Pending
169,personal care,Offline,AB,2023-06-19,1169,C,2023-06-23,120,18,10,India,Asia,Pending
170,household,Online,AC,2023-06-20,1170,P,2023-06-24,80,40,25,France,Europe,Pending
171,cereal,Offline,AD,2023-06-21,1171,S,2023-06-25,90,15,12,Germany,Europe,Pending
172,beverages,Online,A,2023-06-22,1172,C,2023-06-26,70,20,15,South Africa,Africa,Pending
173,meat,Offline,B,2023-06-23,1173,S,2023-06-27,50,50,30,Mexico,North America,Pending
174,vegetables,Online,C,2023-06-24,1174,P,2023-06-28,60,10,8,China,Asia,Pending
175,fruits,Offline,D,2023-06-25,1175,C,2023-06-29,40,35,20,Argentina,South America,Pending
176,snack,Online,A,2023-06-26,1176,S,2023-06-30,30,8,6,United Kingdom,Europe,Pending
177,clothes,Offline,B,2023-06-27,1177,P,2023-07-01,100,25,15,Russia,Europe/Asia,Pending
178,baby food,Online,C,2023-06-28,1178,S,2023-07-02,200,12,8,New Zealand,Oceania,Pending
179,cosmetics,Offline,D,2023-06-29,1179,P,2023-07-03,150,30,20,Spain,Europe,Pending
180,personal care,Online,AB,2023-06-30,1180,S,2023-07-04,120,18,10,Nigeria,Africa,Pending
181,household,Offline,AC,2023-07-01,1181,C,2023-07-05,80,40,25,United States,North America,Pending
182,cereal,Online,AD,2023-07-02,1182,S,2023-07-06,90,15,12,Japan,Asia,Pending
183,beverages,Offline,A,2023-07-03,1183,P,2023-07-07,70,20,15,Italy,Europe,Pending
184,meat,Online,B,2023-07-04,1184,C,2023-07-08,50,50,30,Kenya,Africa,Pending
185,vegetables,Offline,C,2023-07-05,1185,S,2023-07-09,60,10,8,Australia,Oceania,Pending
186,fruits,Online,D,2023-07-06,1186,C,2023-07-10,40,35,20,Brazil,South America,Pending
187,snack,Offline,A,2023-07-07,1187,P,2023-07-11,30,8,6,Egypt,Africa,Pending
188,clothes,Online,B,2023-07-08,1188,S,2023-07-12,100,25,15,Canada,North America,Pending
189,baby food,Offline,C,2023-07-09,1189,S,2023-07-13,200,12,8,India,Asia,Pending
190,cosmetics,Online,D,2023-07-10,1190,P,2023-07-14,150,30,20,France,Europe,Pending
191,personal care,Offline,AB,2023-07-11,1191,C,2023-07-15,120,18,10,Germany,Europe,Pending
192,household,Online,AC,2023-07-12,1192,S,2023-07-16,80,40,25,South Africa,Africa,Pending
193,cereal,Offline,AD,2023-07-13,1193,P,2023-07-17,90,15,12,Mexico,North America,Pending
194,beverages,Online,A,2023-07-14,1194,S,2023-07-18,70,20,15,China,Asia,Pending
195,meat,Offline,B,2023-07-15,1195,S,2023-07-19,50,50,30,Argentina,South America,Pending
196,vegetables,Online,C,2023-07-16,1196,P,2023-07-20,60,10,8,United Kingdom,Europe,Pending
197,fruits,Offline,D,2023-07-17,1197,S,2023-07-21,40,35,20,Russia,Europe/Asia,Pending
198,snack,Online,A,2023-07-18,1198,P,2023-07-22,30,8,6,New Zealand,Oceania,Pending
199,clothes,Offline,B,2023-07-19,1199,C,2023-07-23,100,25,15,Spain,Europe,Pending

```
Atau teman-teman bisa download pada link [Data Dummy](https://docs.google.com/spreadsheets/d/1ce58nsgrWRa8RmFgA77Xrqc5iIODcHgX8pcwllgYsc8/edit?usp=sharing)
Setelah membuat data, atau menguploadnya pastikan nama datanya sesuai ya, atau kita juga bisa menamakan file tersebut sesuai dengan keinginan namun tinggal merubah di definisi saja pada setiap script yang saya buat.

Langkah selanjutnya adalah membuat definisi data

```{r}
# Membaca file CSV dan mendefinisikannya sebagai objek 'data'
data <- read.csv("data_dummy.csv")

# Memeriksa struktur data
str(data)

```

![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/eac51558-05b7-4781-9e8f-4313cbc1dce6)

Setelah itu kita ingin membuat kolom baru sebagai total revenue, total cost dan profit
Dari data di atas kita dapat melihat bahwa belum ada kolom penambahan seperti yang diminta
Maka dari itu kita akan langsung membuat 3 kolom baru seperti:

```{r}
# Menambahkan kolom "total_revenue" dan menghitung nilainya
data <- data %>% 
  mutate(total_revenue = unit_price * unit_sold)

# Menambahkan kolom "total_cost" dan menghitung nilainya
data <- data %>% 
  mutate(total_cost = unit_cost * unit_sold)

# Menambahkan kolom "profit" dan menghitung nilainya
data <- data %>% 
  mutate(profit = total_revenue - total_cost)
```

Kita akan melihat perubahan data dari penambahan 3 kolom seperti pada perintah R di atas
Langkah Selanjutnya adalah melihat data dengan beberapa fungsi seperti summary, head dan tail

```{r}
#melihat 3 tambahan column
str(data)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/0791476f-144a-4fbc-8d71-afc3156e70b7)


```{r}
# summary untuk melihat isi data keseluruhan atau ringkasan data tersebut
summary(data)

```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/a7886d34-1419-4605-b23b-6fc6abbef112)


```{r}
# Fungsi head untuk melihat beberepa kolom pertama
head(data)
# Selain itu kita juga dapat menambahkan jumlah row yang diinginkan
head(data,10)
# dari contoh diatas kita akan melihat 10 baris pertama sesuai dengan intruksi
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/3f4452b3-57ee-426d-93d1-2c254f16f8d6)
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/b21102bd-d724-4a14-85b8-88d2f474a75b)

```{r}
# Fungsi tail untuk melihat beberapa kolom di row terakhir
tail(data,10)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/45ef0a3e-cf7d-4955-ab6a-57dcec071952)

Langkah Selanjutnya adalah membuat pivot dalam RStudio Sebagai Berikut 

```{r}
pivot <- data %>% 
  select(region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(total_profit = sum(profit))
print(pivot)

```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/41e6f40f-a9d0-4179-b005-38466838696b)


Membuat pivot_1 dengan tambahan rata-rata profit

```{r}
pivot_1 <- data %>% 
select(region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(total_profit = sum(profit),avg_profit = mean(profit, na.rm = TRUE))
print(pivot_1)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/6eca2f74-15f7-47ce-801e-a174304bd1d1)

Membuat Pivot ke 3 dengan nama pivot_2 dengan menambahkan total transaksi menghitung dari order_id

```{r}
pivot_2 <- data %>% 
select(order_id, region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(total_profit = sum(profit), avg_profit = mean(profit, na.rm = TRUE), num_trx = count(order_id))
print(pivot_2)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/9e3590ee-5d80-4d43-8c0c-f2108fa17d24)
dari hasil diatas kita dapa melihat bahwa tipe data order id bukan numeric atau integer sehingga fungsi tersebut tidak dapat dijalankan

```{r}
#kita dapat menggantinya dengan fungsi lenght
pivot_2 <- data %>% 
select(order_id, region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(total_profit = sum(profit), avg_profit = mean(profit, na.rm = TRUE), num_trx = length(order_id))
print(pivot_2)

# cara diatas sudah dapat dijalankan namun bisa juga menggunakan fungsi n() atau n_distinct sebagai berikut:

pivot_2 <- data %>% 
  select(order_id, region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(
    total_profit = sum(profit, na.rm = TRUE),
    avg_profit = mean(profit, na.rm = TRUE),
    num_trx = n_distinct(order_id)  # Count distinct order_ids (tapi pada fungsi ini hanya akan menghitung number of unique saja jadi kalo ada dua order_id sama hanya akan dihitung satu)
  )

print(pivot_2)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/a6178128-8fde-4dc7-8d9c-9f11f1a8b765)

Selanjutnya pada pivot ke 3 dengan anama pivot_3 disini saya akan menambahkan fungsi arrange agar dapat mengurutkan number of transaction (jika ada)
```{r}
pivot_3 <- data %>% 
select(order_id, region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(total_profit = sum(profit), avg_profit = mean(profit, na.rm = TRUE), num_trx = length(order_id)) %>% 
  arrange(num_trx)
print(pivot_3)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/a30b8983-6c4f-4f53-8a01-66fd99573a3b)

Dari hasil ini masih belum menampilkan urutan transaksi dari yang terbesar karena R membaca arrange secara ascending (dari yang terkecil ke terbesar atau A-Z)
Selanjutnya menambahkan fungsi DESC setelah fungsi arrange
```{r}
pivot_3 <- data %>% 
select(order_id, region, country, item_type, profit) %>% 
  group_by(region, country, item_type) %>% 
  summarise(total_profit = sum(profit), avg_profit = mean(profit, na.rm = TRUE), num_trx = length(order_id)) %>% 
  arrange(desc(num_trx))
print(pivot_3)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/6622e3b8-a1b5-4cf0-98bd-7ea128698d27)

Dari hasil di atas memang tidak ada total transaksi dari setiap negara terhadap item product yang lebih dari satu kali transaksi(karena masing-masing order_id hanya melakukan satu transaki) jika lebih maka secara otomatis akan muncul dan melakukan perhitungan pada hasil total_profit.
karena dari dataset yang dibuat sebelumnya hanya melakukan satu transaksi


Selanjutnya membuat script untuk pivot tabel sebagai berikut:

```{r}
rpivotTable(data = data, rows = "item_type", cols = "region", vals = "profit", aggregatorName = "Sum", rendererName = "Profit Table", width = "50%", height = "400px")
```
Dengan pivot ini kita dapat melakukan analisa visualisasi dengan pivot chart yang sangat mudah dan menarik.

Analisa Contoh Dengan Tabel dengan item_type pada setiap region 
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/40b98a8f-1429-4a31-82d8-4df07b0a6d0a)

Pada konteks yang sama tabel menggunakan tabel barchart
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/3ad32e5e-88ce-4458-9dbf-4ada65642fe6)

Pada konteks yang sama menggunakan heatmap
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/1e83475f-f9c5-4676-9c8a-515e69d42435)

Pada konteks yang sama menggunakan bar chart
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/d0e1c6ba-19e0-4846-b61d-0710120e59ca)

Pada konteks yang sama menggunakan line chart
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/df9a7eb8-c60a-4a87-b4ed-c2f09ecae0d2)

Dan masih banyak lagi
Sesuai dengan kebutuhan analisa kita masing-masing
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/11f4ba30-d59d-40dd-9532-ff8863e8280b)


## Terima kasih


