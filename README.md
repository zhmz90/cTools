#cTools

This is ~np29/biology/cteam/progs.info
Executables in ~np29/bin
List of accessible samples: /home/np29/cteam/release/cteam.ind
## This is Reich lab only.  Need to make smaller file for public

Two programs (cascertain, cpulldown) to access C team
This is an alpha release and some options surely need to be added.

I use a database I call the "extended C-team" which in addition to the full C team
has high quality ancient genomes:
               Altai  F            Altai
            Denisova  F        Denisovan
           Loschbour  M              WHG
           Stuttgart  F              LBK
           Ust_Ishim  M        Ust_Ishim
## the above are "extended C-team files";  max filter value 1.  Reich lab only (!)
These can be accessed by the software just as though they are part of C-team



1) cascertain -p parfile
Input: criteria to ascertain SNP.   Output .snp file (Reich lab format)

Sample parfile
snpname:      ssout.snp
ascertain:    S_Yoruba-1::1:2,Altai::1:1;S_Yoruba-1::1:2,Denisova::1:1
noascertain:  Altai::1:2,Denisova::1:2

There is a mini-language for ascertainment.  Allele 1 = derived, 0 = ancestral (where Chimp allele is ancestral)
In the ascertainment string we have substrings separated by ';'  each is an ascertainment rule.
Then each rule has substrings separated by ',' ;
Each substring is of form Sample_ID::a:b  This means we require sample to have a derived alleles out of b.

noascertain: has same syntax.   If this "hits" then the SNP is rejected.
Thus the example above means
ascertain if S_Yoruba_1 is a het and either Altai or Denisova has a derived allele (chosen at random)
 EXCEPT don't ascertain if both Altai and Denisova are hets.

C team has base quality in range (0-9) or no value => don't use.
Select bases with
minfilterval: 3 (say)   This selects bases with base quality >=3
1 is default and recommended for most applications.
Note that the extended C-team files such as Altai have manifesto filters (made in Leipzig)
that are just 0, 1.  If you are using extended C -team do not set minfilterval.

=============================================================================================================
2) cpulldown  -p parfile
Input: .snp file (Reich lab format)

Sample parfile
D1:          /home/np29/biology/cteam/mixdir
D2:          D1
S2:           sc
indivname:    D1/mix1.ind
snpname:      D1/s01:01.snp
indivoutname:     D2/S2.ind
snpoutname:       D2/S2.snp
genotypeoutname:  D2/S2.geno
outputformat:     eigenstrat
maxchrom:         22

This is very similar to the parameter file for convertf which most of you will have used.
 indivname should be a .ind file (Reich lab format).
See /home/np29/biology/cteam/info/cteamsmall.ind for the current extended C-team list.
Only 214 samples at present owing to a system crash.  This will be increased to > 290 very shortly.
For now any samples you access should be a subset of cteamsmall.ind.

minfilterval: is a parameter to cpulldown but
*** default is 0 ***;  If you know a marker is truly polymorphic less filtering is justified.
Bugs/complaints to Nick

Of course any .snp file is OK here, it needn't be output from cascertain

Running time: Linear in number of samples in indivname.  10 samples pull down
in about 1 hour on orchestra, so a pull down of the whole C-team is about 24 hours.

3) cpoly
DOCUMENTATION NEEDED

4) ccompress -i sgdpsampname [-w workdir]
Makes files workdir/sgdpampname.comp.fa.gz and workdir/ssgdpname/compmask.fa.gz

5) cuncompress -i sgdpsampname [-w workdir]
Reverse ccompress, but output file left in workdir

6/15/14