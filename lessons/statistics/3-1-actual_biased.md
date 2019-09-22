[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Something like the class size paradox appears if you survey
children and ask how many children are in their family. Families with many
children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.
Now compute the biased distribution we would see if we surveyed the children
and asked them how many children under 18 (including themselves) are in
their household.
Plot the actual and biased distributions, and compute their means. As a
starting place, you can use chap03ex.ipynb.


#read file
resp = nsfg.ReadFemResp()

#actual distribution represented by pmf function, prob mass of families with x num kids
pmf = thinkstats2.Pmf(resp.numkdhh, label='numkdhh')

#plot the actual distribution
thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

#use bias function, involves multiplying the probabilities by the number who report it, and then normalizing. 
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        new_pmf.Normalize()
    return new_pmf

biased = BiasPmf(pmf, label='biased')

#plot the biased distribution
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

#take mean of values of the actual and biased data and cmpare
pmf.Mean()
biased.Mean()
