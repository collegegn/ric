# ric
-----------------------[PRACTICAL 1]----------------

import pandas as pd

d={'Age':pd.Series([25,26,25,23,30,29,23,34,40,30,51,46]),

'Rating':pd.Series([4.23,3.24,3.98,2.56,3.20,4.6,3.8,3.78,2.98,4.80,4.10,3.65])}

df=pd.DataFrame(d)

print(df)


print(df.sum())

print(df.mean())

print(df.std())

print(df.describe())


---------------{CHI SQUARE TEST}-------------------


import numpy as np

import pandas as pd

import scipy.stats as stats

np.random.seed(10)

stud_grade = np.random.choice(a=["O","A","B","C","D"],p=[0.20,0.20,0.20,0.20,0.20],size=100)



stud_gen=np.random.choice(a=["Male","Female"],p=[0.5,0.5],size=100)



mscpart1=pd.DataFrame({"Grades":stud_grade,"Gender":stud_gen})

print(mscpart1)



stud_tab=pd.crosstab(mscpart1.Grades,mscpart1.Gender,margins=True)



stud_tab.columns= ["Male","Female", "row_totals"]

stud_tab.index=["O","A","B","C","D","col_totals"]



observed=stud_tab.iloc[0:5,0:2]

print(observed)



expected=np.outer(stud_tab["row_totals"][0:5],stud_tab.loc["col_totals"][0:2])/100

print(expected)



chi_squared_test=(((observed-expected)**2)/expected).sum().sum()

print('Calculated: ',chi_squared_test)



crit=stats.chi2.ppf(q=0.95,df=4)



print('Table Value:',crit)

if chi_squared_test>=crit:


print("H0 is accepted")
   

else:

print("H0 is rejected")


-----------------------[MEAN DIST SIGNIFICATION]----------------------------


import numpy as np

from scipy import stats

from numpy.random import randn

N=20

#a=[35,40,12,15,21,14,46,10,28,48,16,30,32,48,31,22,12,39,19,25]



a=5* randn(100) +50

b=5* randn(100) +51



var_a=a.var(ddof=1)

var_b = b.var(ddof=1)


s=np.sqrt((var_a + var_b)/2)

t=(a.mean()-b.mean())/(s*np.sqrt(2/N))

df=2*N-2

p=1-stats.t.cdf(t,df=df)

print("t=" +str(t))

print("p=" +str(2*p))

if t>p:

print("mean of two distribution are different and significant")

else:

print("mean of two distribution are same and not significant")


----------------------[T TEST]-------------------------------


from scipy.stats import ttest_1samp #one 1 (not L) 

import numpy as np

file=open("S:/ages.csv")

ages=np.loadtxt(file,delimiter=",")

print(ages)


ages_mean=np.mean(ages)

test,pval=ttest_1samp(ages,30)

print('p=value-',pval)

if pval<0.05:

print("we are rejecting null hypothesis")

else:

print("we are accepting null hypothesis")

------------------[BELL SHAPE]-------------------------------

Age	Male	Female	Total	Male%	Female%	

0-4	328759	307079	635838	-4.761250981	4.447270462	

5-9	315119	293664	608783	-4.563709732	4.252987775	

10-14	311456	290598	602054	-4.510660348	4.208584442	

15-19	321831	293313	615144	-4.660916247	4.247904419	

20-24	311077	295739	606816	-4.505171482	4.283038955	

25-29	284258	273379	557637	-4.116765416	3.959210339	

30-34	255596	247383	502979	-3.701668108	3.582723367	

35-39	248575	241938	490513	-3.599986502	3.503866175	

40-44	232217	226914	459131	-3.363081829	3.286281151	

45-49	202633	201142	403775	-2.93463166	2.913038258	

50-54	176241	176440	352681	-2.552409619	2.555291636	

55-59	153494	156283	309777	-2.222976278	2.26336796	

60-64	114194	121200	235394	-1.653814175	1.755278544	

65-69	83,129	92071	175,200	-1.20391543	1.333417911	

70-74	65,266	77990	143,256	-0.9452145995	1.129489882	

75-79	43,761	56895	100,656	-0.6337685179	0.8239816235	

80-84	25,060	37873	62,933	-0.3629313557	0.54849558	

85+	14,164	28156	42,320	-0.2051300767	0.4077691641	

total	3486830	3418057	6904887	-50.49800236	49.50199764	








