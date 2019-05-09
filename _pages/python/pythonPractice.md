---
layout: page
title: "Python Practice"
permalink: /python/pythonPractice/
tags: [ Python, survival guide ]
description: Python Practice page
---

| Description | Hands On Lab Exercises for Python |
| :------------- | :------------- | :------------- | :------------- |
| Related-course materials | [Python introduction](https://southgreenplatform.github.io/trainings//python/) |
| Authors | Sébastien RAVEL (sebastien.ravel@cirad.fr)<br/>
            Christine TRANCHANT (christine.tranchant@ird.fr)  |
| Creation Date | 2017 |
| Last Modified Date | 13/05/2019  |


-----------------------

### Summary

* [Exercice 1](#practice-1)

* [Links](#links)
* [License](#license)


-----------------------

<a name="practice-1"></a>
### Exercice 1 :

En mode interactif, demander à l'interpréteur de calculer
```python
5*6    
10/3               
10.0/3.0         
print("Hello world !")
```

Rappel mode interactif
ouvrir un terminal    
lancer l'interpréteur python via la commande python
taper les instructions souhaitées

#### <a name="order"></a>Providing an order
The order of a pipeline is provided with key <b>$order</b>, base on the file, build new config file to run only from mapping to SNP calling.


#### <a name="TPcluster"></a>TP on IRD cluster

All input data:
* Input data : /data2/formation/TPsnpSV/fastqDir/
* Reference : /data2/formation/TPsnpSV/reference.fasta
* Config file: /data2/formation/TPsnpSV/configFiles/SNPdiscoveryPaired.config.txt

To do:
* Create a "formationX" directory in your account
* Make à copy for reference and input data into "formationX" directory (scp).
* Add the configuration file used by Python and change SGE key as below
{% highlight bash %}
$sge
-q formation.q
-b Y
-cwd
{% endhighlight %}


##### Connect to account and prepare datas:

* Connect to the cluster:
{% highlight bash %}
    ssh -Y formationX@bioinfo-master.ird.fr
{% endhighlight %}
* Launch a QRSH command:
{% highlight bash %}
    qrsh -q formation.q
{% endhighlight %}
* Transfer the data from nas using SCP:
{% highlight bash %}
    scp -r nas:/data2/formation/TPsnpSV .
{% endhighlight %}
* Load Python tools:
{% highlight bash %}
    module load bioinfo/Python/0.3.6
{% endhighlight %}


-----------------------

#### Launching an analysis

Use only one script to run all pipeline: <b>PythonGenerator.pl</b> script usage

{% highlight bash %}
  PythonGenerator.pl -d|--directory DIR -c|--config FILE -o|--outputdir DIR [-r|--reference FILE] [-k|--keyfile FILE] [-g|--gff FILE] [-nocheck|--nocheckFastq] [--help|-h]
{% endhighlight %}

| Required named arguments:       |                                                                                                                                |
| :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------- |
| -d / --directory DIR:           | a folder with raw data to be treated (FASTQ, FASTQ.GZ, SAM, BAM, VCF)                                                          |
| -c / --config FILE:             | generally it is the *software.config.txt* file but it can be any text file structured as shown below.                          |
| -o / --outputdir DIR:           | the current version of Python will not modify the initial data folder but will create an output directory with all analyses in.|

| Optional named arguments:       |                                                                                                                                |
| :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------- |
| -r / --reference FILE:          | the reference FASTA file to be used. (1)                                                                                           |
| -g / -gff FILE:                 | the GFF file to be used for some tools.                                                                                        |
| -k / --keyfile FILE:            | the keyfile use for demultiplexing step.                                                                                       |
| -nocheck / --nocheckFastq:      | by default Python checks if fastq format is correct in every file. This option allows to skip this step.                       |
| -report / --report:      | generate pdf report <a href="{{ site.url }}/manual/completeManual/#report">(more info)</a>                        |
| -h / --help:                    | show help message and exit                                                                                                     |

(1): If no database index exists, it will be automatically created if it is necessary. If the index already exists, they will not be re-created UNLESS the pipeline order (see below) expressively requests it (updating the index e.g.)

All the the paths (files and folders) can be provided as absolute (/home/mylogin/data/myRef.fasta) or relative (../data/myRef.fasta).

Example of a command to run Python :
{% highlight bash %}
PythonGenerator.pl -d ~/Python/fastq -c ~/Python/SNPdiscoveryPaired.config.txt -o ~/Python/outputRES -r ~/Python/reference.fasta -nocheck -report
{% endhighlight %}
 
-----------------------



SOLUTIONS:

{% highlight bash %}
vim SNPdiscoveryPaired.config.txt
 qsub -q formation.q -b Y -N Python "module load bioinfo/Python/0.3.6; PythonGenerator.pl -c /home/formationX/TPsnpSV/configFiles/SNPdiscoveryPaired.config.txt -d /home/formationX/TPsnpSV/fastqDir/ -r /home/formationX/TPsnpSV/reference.fasta -o /home/formationX/outputPython -nocheck -report"
{% endhighlight %}




-----------------------

### Links
<a name="links"></a>

* Related courses : [Python]({{ site.url }}/Python)

-----------------------

### License
<a name="license"></a>

<div>
The resource material is licensed under the Creative Commons Attribution 4.0 International License (<a href="http://creativecommons.org/licenses/by-nc-sa/4.0/">here</a>).
<center><img width="25%" class="img-responsive" src="http://creativecommons.org.nz/wp-content/uploads/2012/05/by-nc-sa1.png"/>
</center>
</div>
                  
 