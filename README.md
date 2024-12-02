import sys #Completing tasks for part 1
import statistics
import pandas as pd
import matplotlib.pyplot as ax
file = open("PFAS_Course_Project.csv", "r")

count = 0
x = 0
means = []
medians = []
deviations = []
titles = ["PFBA 2019", "PFBA 2021", "PFBS 2019", "PFBS 2021", "PFPeA 2019", "PFPeA 2021", "PFPeS 2019", "PFPeS 2021", "PFHxA 2019", "PFHxA 2021", "PFHxS 2019", "PFHxS 2021", "PFHxPA 2019", "PFHxPA 2021", "PFHpA 2019", "PFHpA 2021", "Oak 6 2019", "Oak 6 2021", "PFHpS 2019", "PFHpS 2021", "Syn 53 2019", "Syn 53 2021", "P4MOA 2019", "P4MOA 2021", "PFOA 2019", "PFOA 2021", "L-PFOS 2019", "L-PFOS 2021", "BrPFOS 2019", "BrPFOS 2021", "PFNA 2019", "PFNA 2021", "PFUdA 2019", "PFUdA 2021", "PFDA 2019", "PFDA 2021", "PFDoA 2019", "PFDoA 2021", "N-etFOSAA 2019", "N-etFOSAA 2021"]
header = file.readline().strip().split(",")

for line in file:
    data = line.strip().split(",")
    data[2] = float(data[2])
    data[3] = float(data[3])
    data[4] = float(data[4])
    data[5] = float(data[5])
    data[6] = float(data[6])
    data[7] = float(data[7])
    data[8] = float(data[8])
    data[9] = float(data[9])
    data[10] = float(data[10])
    data[11] = float(data[11])
    data[12] = float(data[12])
    year_means = statistics.mean(data[2:12])
    year_medians = statistics.median(data[2:12])
    year_devs = statistics.stdev(data[2:12])
    medians.append(year_medians)
    means.append(year_means)
    deviations.append(year_devs)
    ax.figure()
    ax.hist(data[2:12], bins=11)
    ax.title(titles[count])
    ax.xlabel("Concentration (ng/L)")
    ax.ylabel("Frequency")
    ax.grid(True)
    ax.show()
    count = count + 1
    
while x < 40:
    print("The mean, median, and mode for %s are %f, %f, and %f respectively" %(titles[x], means[x], medians[x], deviations[x]))
    x = x + 1
    
file.close

import sys #Completing tasks for part 2
from scipy import stats
import pandas as pd
import matplotlib.pyplot as ax
import numpy as np
file = open("PFAS_Course_Project.csv", "r")

lists = []
titles = ["PFBA 2019", "PFBA 2021", "PFBS 2019", "PFBS 2021", "PFPeA 2019", "PFPeA 2021", "PFPeS 2019", "PFPeS 2021", "PFHxA 2019", "PFHxA 2021", "PFHxS 2019", "PFHxS 2021", "PFHxPA 2019", "PFHxPA 2021", "PFHpA 2019", "PFHpA 2021", "Oak 6 2019", "Oak 6 2021", "PFHpS 2019", "PFHpS 2021", "Syn 53 2019", "Syn 53 2021", "P4MOA 2019", "P4MOA 2021", "PFOA 2019", "PFOA 2021", "L-PFOS 2019", "L-PFOS 2021", "BrPFOS 2019", "BrPFOS 2021", "PFNA 2019", "PFNA 2021", "PFUdA 2019", "PFUdA 2021", "PFDA 2019", "PFDA 2021", "PFDoA 2019", "PFDoA 2021", "N-etFOSAA 2019", "N-etFOSAA 2021"]
header = file.readline().strip().split(",")

for line in file:
    data = line.strip().split(",")
    values = list(map(float, data[2:13]))
    lists.append(values)
    
PFBA_19 = lists[0]
PFBA_21 = lists[1]
PFBS_19 = lists[2]
PFBS_21 = lists[3]
PFPeA_19 = lists[4]
PFPeA_21 = lists[5]
PFPeS_19 = lists[6]
PFPeS_21 = lists[7]
PFHxA_19 = lists[8]
PFHxA_21 = lists[9]
PFHxS_19 = lists[10]
PFHxS_21 = lists[11]
PFHxPA_19 = lists[12]
PFHxPA_21 = lists[13]
PFHpA_19 = lists[14]
PFHpA_21 = lists[15]
Oak6_19 = lists[16]
Oak6_21 = lists[17]
PFHpS_19 = lists[18]
PFHpS_21 = lists[19]
Syn53_19 = lists[20]
Syn53_21 = lists[21]
P4MOA_19 = lists[22]
P4MOA_21 = lists[23]
PFOA_19 = lists[24]
PFOA_21 = lists[25]
LPFOS_19 = lists[26]
LPFOS_21 = lists[27]
BrPFOS_19 = lists[28]
BrPFOS_21 = lists[29]
PFNA_19 = lists[30]
PFNA_21 = lists[31]
PFUdA_19 = lists[32]
PFUdA_21 = lists[33]
PFDA_19 = lists[34]
PFDA_21 = lists[35]
PFDoA_19 = lists[36]
PFDoA_21 = lists[37]
NetFOSAA_19 = lists[38]
NetFOSAA_21 = lists[39] 

PFBA_pearson = stats.pearsonr(PFBA_19, PFBA_21)
PFBA_spearman = stats.spearmanr(PFBA_19, PFBA_21)
PFBA_slope, PFBA_intercept, x, y, z = stats.linregress(PFBA_19, PFBA_21)
x_PFBA = np.linspace(min(PFBA_19), max(PFBA_19), 100)
y_PFBA = PFBA_slope * x_PFBA + PFBA_intercept
PFBA_LR = stats.linregress(PFBA_19, PFBA_21)

PFBS_pearson = stats.pearsonr(PFBS_19, PFBS_21)
PFBS_spearman = stats.spearmanr(PFBS_19, PFBS_21)
PFBS_slope, PFBS_intercept, x, y, z = stats.linregress(PFBS_19, PFBS_21)
x_PFBS = np.linspace(min(PFBS_19), max(PFBS_19), 100)
y_PFBS = PFBS_slope * x_PFBS + PFBS_intercept
PFBS_LR = stats.linregress(PFBS_19, PFBS_21)

PFPeA_pearson = stats.pearsonr(PFPeA_19, PFPeA_21)
PFPeA_spearman = stats.spearmanr(PFPeA_19, PFPeA_21)
PFPeA_slope, PFPeA_intercept, x, y, z = stats.linregress(PFPeA_19, PFPeA_21)
x_PFPeA = np.linspace(min(PFPeA_19), max(PFPeA_19), 100)
y_PFPeA = PFPeA_slope * x_PFPeA + PFPeA_intercept
PFPeA_LR = stats.linregress(PFPeA_19, PFPeA_21)

PFPeS_pearson = stats.pearsonr(PFPeS_19, PFPeS_21)
PFPeS_spearman = stats.spearmanr(PFPeS_19, PFPeS_21)
PFPeS_slope, PFPeS_intercept, x, y, z = stats.linregress(PFPeS_19, PFPeS_21)
x_PFPeS = np.linspace(min(PFPeS_19), max(PFPeS_19), 100)
y_PFPeS = PFPeS_slope * x_PFPeS + PFPeS_intercept
PFPeS_LR = stats.linregress(PFPeS_19, PFPeS_21)

PFHxA_pearson = stats.pearsonr(PFHxA_19, PFHxA_21)
PFHxA_spearman = stats.spearmanr(PFHxA_19, PFHxA_21)
PFHxA_slope, PFHxA_intercept, x, y, z = stats.linregress(PFHxA_19, PFHxA_21)
x_PFHxA = np.linspace(min(PFHxA_19), max(PFHxA_19), 100)
y_PFHxA = PFHxA_slope * x_PFHxA + PFHxA_intercept
PFHxA_LR = stats.linregress(PFHxA_19, PFHxA_21)

PFHxS_pearson = stats.pearsonr(PFHxS_19, PFHxS_21)
PFHxS_spearman = stats.spearmanr(PFHxS_19, PFHxS_21)
PFHxS_slope, PFHxS_intercept, x, y, z = stats.linregress(PFHxS_19, PFHxS_21)
x_PFHxS = np.linspace(min(PFHxS_19), max(PFHxS_19), 100)
y_PFHxS = PFHxS_slope * x_PFHxS + PFHxS_intercept
PFHxS_LR = stats.linregress(PFHxS_19, PFHxS_21)

PFHxPA_pearson = stats.pearsonr(PFHxPA_19, PFHxPA_21)
PFHxPA_spearman = stats.spearmanr(PFHxPA_19, PFHxPA_21)
PFHxPA_slope, PFHxPA_intercept, x, y, z = stats.linregress(PFHxPA_19, PFHxPA_21)
x_PFHxPA = np.linspace(min(PFHxPA_19), max(PFHxPA_19), 100)
y_PFHxPA = PFHxPA_slope * x_PFHxPA + PFHxPA_intercept
PFHxPA_LR = stats.linregress(PFHxPA_19, PFHxPA_21)

PFHpA_pearson = stats.pearsonr(PFHpA_19, PFHpA_21)
PFHpA_spearman = stats.spearmanr(PFHpA_19, PFHpA_21)
PFHpA_slope, PFHpA_intercept, x, y, z = stats.linregress(PFHpA_19, PFHpA_21)
x_PFHpA = np.linspace(min(PFHpA_19), max(PFHpA_19), 100)
y_PFHpA = PFHpA_slope * x_PFHpA + PFHpA_intercept
PFHpA_LR = stats.linregress(PFHpA_19, PFHpA_21)

Oak6_pearson = stats.pearsonr(Oak6_19, Oak6_21)
Oak6_spearman = stats.spearmanr(Oak6_19, Oak6_21)

PFHpS_pearson = stats.pearsonr(PFHpS_19, PFHpS_21)
PFHpS_spearman = stats.spearmanr(PFHpS_19, PFHpS_21)
PFHpS_slope, PFHpS_intercept, x, y, z = stats.linregress(PFHpS_19, PFHpS_21)
x_PFHpS = np.linspace(min(PFHpS_19), max(PFHpS_19), 100)
y_PFHpS = PFHpS_slope * x_PFHpS + PFHpS_intercept
PFHpS_LR = stats.linregress(PFHpS_19, PFHpS_21)

Syn53_pearson = stats.pearsonr(Syn53_19, Syn53_21)
Syn53_spearman = stats.spearmanr(Syn53_19, Syn53_21)

P4MOA_pearson = stats.pearsonr(P4MOA_19, P4MOA_21)
P4MOA_spearman = stats.spearmanr(P4MOA_19, P4MOA_21)

PFOA_pearson = stats.pearsonr(PFOA_19, PFOA_21)
PFOA_spearman = stats.spearmanr(PFOA_19, PFOA_21)
PFOA_slope, PFOA_intercept, x, y, z = stats.linregress(PFOA_19, PFOA_21)
x_PFOA = np.linspace(min(PFOA_19), max(PFOA_19), 100)
y_PFOA = PFOA_slope * x_PFOA + PFOA_intercept
PFOA_LR = stats.linregress(PFOA_19, PFOA_21)

LPFOS_pearson = stats.pearsonr(LPFOS_19, LPFOS_21)
LPFOS_spearman = stats.spearmanr(LPFOS_19, LPFOS_21)
LPFOS_slope, LPFOS_intercept, x, y, z = stats.linregress(LPFOS_19, LPFOS_21)
x_LPFOS = np.linspace(min(LPFOS_19), max(LPFOS_19), 100)
y_LPFOS = LPFOS_slope * x_LPFOS + LPFOS_intercept
LPFOS_LR = stats.linregress(LPFOS_19, LPFOS_21)

BrPFOS_pearson = stats.pearsonr(BrPFOS_19, BrPFOS_21)
BrPFOS_spearman = stats.spearmanr(BrPFOS_19, BrPFOS_21)
BrPFOS_slope, BrPFOS_intercept, x, y, z = stats.linregress(BrPFOS_19, BrPFOS_21)
x_BrPFOS = np.linspace(min(BrPFOS_19), max(BrPFOS_19), 100)
y_BrPFOS = BrPFOS_slope * x_BrPFOS + BrPFOS_intercept
BrPFOS_LR = stats.linregress(BrPFOS_19, BrPFOS_21)

PFNA_pearson = stats.pearsonr(PFNA_19, PFNA_21)
PFNA_spearman = stats.spearmanr(PFNA_19, PFNA_21)
PFNA_slope, PFNA_intercept, x, y, z = stats.linregress(PFNA_19, PFNA_21)
x_PFNA = np.linspace(min(PFNA_19), max(PFNA_19), 100)
y_PFNA = PFNA_slope * x_PFNA + PFNA_intercept
PFNA_LR = stats.linregress(PFNA_19, PFNA_21)

PFUdA_pearson = stats.pearsonr(PFUdA_19, PFUdA_21)
PFUdA_spearman = stats.spearmanr(PFUdA_19, PFUdA_21)
PFUdA_slope, PFUdA_intercept, x, y, z = stats.linregress(PFUdA_19, PFUdA_21)
x_PFUdA = np.linspace(min(PFUdA_19), max(PFUdA_19), 100)
y_PFUdA = PFUdA_slope * x_PFUdA + PFUdA_intercept
PFUdA_LR = stats.linregress(PFUdA_19, PFUdA_21)

PFDA_pearson = stats.pearsonr(PFDA_19, PFDA_21)
PFDA_spearman = stats.spearmanr(PFDA_19, PFDA_21)
PFDA_slope, PFDA_intercept, x, y, z = stats.linregress(PFDA_19, PFDA_21)
x_PFDA = np.linspace(min(PFDA_19), max(PFDA_19), 100)
y_PFDA = PFDA_slope * x_PFDA + PFDA_intercept
PFDA_LR = stats.linregress(PFDA_19, PFDA_21)

PFDoA_pearson = stats.pearsonr(PFDoA_19, PFDoA_21)
PFDoA_spearman = stats.spearmanr(PFDoA_19, PFDoA_21)
PFDoA_slope, PFDoA_intercept, x, y, z = stats.linregress(PFDoA_19, PFDoA_21)
x_PFDoA = np.linspace(min(PFDoA_19), max(PFDoA_19), 100)
y_PFDoA = PFDoA_slope * x_PFDoA + PFDoA_intercept
PFDoA_LR = stats.linregress(PFDoA_19, PFDoA_21)

NetFOSAA_pearson = stats.pearsonr(NetFOSAA_19, NetFOSAA_21)
NetFOSAA_spearman = stats.spearmanr(NetFOSAA_19, NetFOSAA_21)
NetFOSAA_slope, NetFOSAA_intercept, x, y, z = stats.linregress(NetFOSAA_19, NetFOSAA_21)
x_NetFOSAA = np.linspace(min(NetFOSAA_19), max(NetFOSAA_19), 100)
y_NetFOSAA = NetFOSAA_slope * x_NetFOSAA + NetFOSAA_intercept
NetFOSAA_LR = stats.linregress(NetFOSAA_19, NetFOSAA_21)

ax.figure()
ax.scatter(PFBA_19, PFBA_21)
ax.title("Correlation Between 2019 and 2021 PFBA Concentration (ng/L)")
ax.plot(x_PFBA, y_PFBA, color='red') 
ax.xlabel("PFBA 2019")
ax.ylabel("PFBA 2021")

ax.figure()
ax.scatter(PFBS_19, PFBS_21)
ax.title("Correlation Between 2019 and 2021 PFBS Concentration (ng/L)")
ax.plot(x_PFBS, y_PFBS, color='red') 
ax.xlabel("PFBS 2019")
ax.ylabel("PFBS 2021")

ax.figure()
ax.scatter(PFPeA_19, PFPeA_21)
ax.title("Correlation Between 2019 and 2021 PFPeA Concentration (ng/L)")
ax.plot(x_PFPeA, y_PFPeA, color='red') 
ax.xlabel("PFPeA 2019")
ax.ylabel("PFPeA 2021")

ax.figure()
ax.scatter(PFPeS_19, PFPeS_21)
ax.title("Correlation Between 2019 and 2021 PFPeS Concentration (ng/L)")
ax.plot(x_PFPeS, y_PFPeS, color='red') 
ax.xlabel("PFPeS 2019")
ax.ylabel("PFPeS 2021")

ax.figure()
ax.scatter(PFHxA_19, PFHxA_21)
ax.title("Correlation Between 2019 and 2021 PFHxA Concentration (ng/L)")
ax.plot(x_PFHxA, y_PFHxA, color='red') 
ax.xlabel("PFHxA 2019")
ax.ylabel("PFHxA 2021")

ax.figure()
ax.scatter(PFHxS_19, PFHxS_21)
ax.title("Correlation Between 2019 and 2021 PFHxS Concentration (ng/L)")
ax.plot(x_PFHxS, y_PFHxS, color='red') 
ax.xlabel("PFHxS 2019")
ax.ylabel("PFHxS 2021")

ax.figure()
ax.scatter(PFHxPA_19, PFHxPA_21)
ax.title("Correlation Between 2019 and 2021 PFHxPA Concentration (ng/L)")
ax.plot(x_PFHxPA, y_PFHxPA, color='red') 
ax.xlabel("PFHxPA 2019")
ax.ylabel("PFHxPA 2021")

ax.figure()
ax.scatter(PFHpA_19, PFHpA_21)
ax.title("Correlation Between 2019 and 2021 PFHpA Concentration (ng/L)")
ax.plot(x_PFHpA, y_PFHpA, color='red') 
ax.xlabel("PFHpA 2019")
ax.ylabel("PFHpA 2021")

ax.figure()
ax.scatter(Oak6_19, Oak6_21)
ax.title("Correlation Between 2019 and 2021 Oak 6 Concentration (ng/L)")
ax.xlabel("Oak 6 2019")
ax.ylabel("Oak 6 2021")

ax.figure()
ax.scatter(PFHpS_19, PFHpS_21)
ax.title("Correlation Between 2019 and 2021 PFHpS Concentration (ng/L)")
ax.plot(x_PFHpS, y_PFHpS, color='red') 
ax.xlabel("PFHpS 2019")
ax.ylabel("PFHpS 2021")

ax.figure()
ax.scatter(Syn53_19, Syn53_21)
ax.title("Correlation Between 2019 and 2021 Syn 53 Concentration (ng/L)") 
ax.xlabel("Syn 53 2019")
ax.ylabel("Syn 53 2021")

ax.figure()
ax.scatter(P4MOA_19, P4MOA_21)
ax.title("Correlation Between 2019 and 2021 P4MOA Concentration (ng/L)") 
ax.xlabel("P4MOA 2019")
ax.ylabel("P4MOA 2021")

ax.figure()
ax.scatter(PFOA_19, PFOA_21)
ax.title("Correlation Between 2019 and 2021 PFOA Concentration (ng/L)")
ax.plot(x_PFOA, y_PFOA, color='red') 
ax.xlabel("PFOA 2019")
ax.ylabel("PFOA 2021")

ax.figure()
ax.scatter(LPFOS_19, LPFOS_21)
ax.title("Correlation Between 2019 and 2021 LPFOS Concentration (ng/L)")
ax.plot(x_LPFOS, y_LPFOS, color='red') 
ax.xlabel("LPFOS 2019")
ax.ylabel("LPFOS 2021")

ax.figure()
ax.scatter(BrPFOS_19, BrPFOS_21)
ax.title("Correlation Between 2019 and 2021 BrPFOS Concentration (ng/L)")
ax.plot(x_BrPFOS, y_BrPFOS, color='red') 
ax.xlabel("BrPFOS 2019")
ax.ylabel("BrPFOS 2021")

ax.figure()
ax.scatter(PFNA_19, PFNA_21)
ax.title("Correlation Between 2019 and 2021 PFNA Concentration (ng/L)")
ax.plot(x_PFNA, y_PFNA, color='red') 
ax.xlabel("PFNA 2019")
ax.ylabel("PFNA 2021")

ax.figure()
ax.scatter(PFUdA_19, PFUdA_21)
ax.title("Correlation Between 2019 and 2021 PFUdA Concentration (ng/L)")
ax.plot(x_PFUdA, y_PFUdA, color='red') 
ax.xlabel("PFUdA 2019")
ax.ylabel("PFUdA 2021")

ax.figure()
ax.scatter(PFDA_19, PFDA_21)
ax.title("Correlation Between 2019 and 2021 PFDA Concentration (ng/L)")
ax.plot(x_PFDA, y_PFDA, color='red') 
ax.xlabel("PFDA 2019")
ax.ylabel("PFDA 2021")

ax.figure()
ax.scatter(PFDoA_19, PFDoA_21)
ax.title("Correlation Between 2019 and 2021 PFDoA Concentration (ng/L)")
ax.plot(x_PFDoA, y_PFDoA, color='red') 
ax.xlabel("PFDoA 2019")
ax.ylabel("PFDoA 2021")

ax.figure()
ax.scatter(NetFOSAA_19, NetFOSAA_21)
ax.title("Correlation Between 2019 and 2021 NetFOSAA Concentration (ng/L)")
ax.plot(x_NetFOSAA, y_NetFOSAA, color='red') 
ax.xlabel("NetFOSAA 2019")
ax.ylabel("NetFOSAA 2021")

print("The pearson and spearman coefficients for PFBA 2019 and 2021 are %f and %f respectively" %(PFBA_pearson.statistic, PFBA_spearman.statistic))
print("The linear regression results for PFBA are below:")
print(PFBA_LR)

print("The pearson and spearman coefficients for PFBS 2019 and 2021 are %f and %f respectively" %(PFBS_pearson.statistic, PFBS_spearman.statistic))
print("The linear regression results for PFBS are below:")
print(PFBS_LR)

print("The pearson and spearman coefficients for PFPeA 2019 and 2021 are %f and %f respectively" %(PFPeA_pearson.statistic, PFPeA_spearman.statistic))
print("The linear regression results for PFPeA are below:")
print(PFPeA_LR)

print("The pearson and spearman coefficients for PFPeS 2019 and 2021 are %f and %f respectively" %(PFPeS_pearson.statistic, PFPeS_spearman.statistic))
print("The linear regression results for PFPeS are below:")
print(PFPeS_LR)

print("The pearson and spearman coefficients for PFHxA 2019 and 2021 are %f and %f respectively" %(PFHxA_pearson.statistic, PFHxA_spearman.statistic))
print("The linear regression results for PFHxA are below:")
print(PFHxA_LR)

print("The pearson and spearman coefficients for PFHxS 2019 and 2021 are %f and %f respectively" %(PFHxS_pearson.statistic, PFHxS_spearman.statistic))
print("The linear regression results for PFHxS are below:")
print(PFHxS_LR)

print("The pearson and spearman coefficients for PFHxPA 2019 and 2021 are %f and %f respectively" %(PFHxPA_pearson.statistic, PFHxPA_spearman.statistic))
print("The linear regression results for PFHxPA are below:")
print(PFHxPA_LR)

print("The pearson and spearman coefficients for PFHpA 2019 and 2021 are %f and %f respectively" %(PFHpA_pearson.statistic, PFHpA_spearman.statistic))
print("The linear regression results for PFHpA are below:")
print(PFHpA_LR)

print("The pearson and spearman coefficients for Oak 6 2019 and 2021 are %f and %f respectively" %(Oak6_pearson.statistic, Oak6_spearman.statistic))

print("The pearson and spearman coefficients for PFHpS 2019 and 2021 are %f and %f respectively" %(PFHpS_pearson.statistic, PFHpS_spearman.statistic))
print("The linear regression results for PFHpS are below:")
print(PFHpS_LR)

print("The pearson and spearman coefficients for Syn 53 2019 and 2021 are %f and %f respectively" %(Syn53_pearson.statistic, Syn53_spearman.statistic))

print("The pearson and spearman coefficients for P4MOA 2019 and 2021 are %f and %f respectively" %(P4MOA_pearson.statistic, P4MOA_spearman.statistic))

print("The pearson and spearman coefficients for PFOA 2019 and 2021 are %f and %f respectively" %(PFOA_pearson.statistic, PFOA_spearman.statistic))
print("The linear regression results for PFOA are below:")
print(PFOA_LR)

print("The pearson and spearman coefficients for LPFOS 2019 and 2021 are %f and %f respectively" %(LPFOS_pearson.statistic, LPFOS_spearman.statistic))
print("The linear regression results for LPFOS are below:")
print(LPFOS_LR)

print("The pearson and spearman coefficients for BrPFOS 2019 and 2021 are %f and %f respectively" %(BrPFOS_pearson.statistic, BrPFOS_spearman.statistic))
print("The linear regression results for BrPFOS are below:")
print(BrPFOS_LR)

print("The pearson and spearman coefficients for PFNA 2019 and 2021 are %f and %f respectively" %(PFNA_pearson.statistic, PFNA_spearman.statistic))
print("The linear regression results for PFNA are below:")
print(PFNA_LR)

print("The pearson and spearman coefficients for PFUdA 2019 and 2021 are %f and %f respectively" %(PFUdA_pearson.statistic, PFUdA_spearman.statistic))
print("The linear regression results for PFUdA are below:")
print(PFUdA_LR)

print("The pearson and spearman coefficients for PFDA 2019 and 2021 are %f and %f respectively" %(PFDA_pearson.statistic, PFDA_spearman.statistic))
print("The linear regression results for PFDA are below:")
print(PFDA_LR)

print("The pearson and spearman coefficients for PFDoA 2019 and 2021 are %f and %f respectively" %(PFDoA_pearson.statistic, PFDoA_spearman.statistic))
print("The linear regression results for PFDoA are below:")
print(PFDoA_LR)

print("The pearson and spearman coefficients for NetFOSAA 2019 and 2021 are %f and %f respectively" %(NetFOSAA_pearson.statistic, NetFOSAA_spearman.statistic))
print("The linear regression results for NetFOSAA are below:")
print(NetFOSAA_LR)

file.close()

import sys #Completing tasks for part 3
from scipy import stats
import pandas as pd
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler
import matplotlib.pyplot as ax
import numpy as np
file = open("PFAS_Course_Project.csv", "r")

lists = []

header = file.readline().strip().split(",")

for line in file:
    data = line.strip().split(",")
    values = list(map(float, data[2:13]))
    lists.append(values)

df = pd.DataFrame(lists)
scaler = StandardScaler()
scaled = scaler.fit_transform(df)
pca = PCA(n_components=2)
pca.fit(scaled)
weights = pca.components_
principal_components = pca.fit_transform(lists)

ax.figure()
ax.bar(df.columns, weights[0])
ax.title("Principal Component Weights") 
ax.xlabel("Principal Component")
ax.ylabel("Weight")

ax.figure()
ax.scatter(principal_components[:,0], principal_components[:,1])
ax.title("PCA Plot")
ax.xlabel("PC1 (" + str(np.round(pca.explained_variance_ratio_[0]*100, decimals=2)) + "%)")
ax.ylabel("PC2 (" + str(np.round(pca.explained_variance_ratio_[1]*100, decimals=2)) + "%)")
