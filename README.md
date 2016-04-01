# Tip and tricks for IBM platform LSF HPC job scheduler

Warning: some information might be specific to IARC HPC cluster.

## Useful links
Official IBM [documentation](https://www.ibm.com/support/knowledgecenter/#!/SSETD4/product_welcome_lsf.html)

## Run jobs

## Monitor jobs

## Administration
In /opt/lsf/conf/lsbatch/cluster_name/configdir/lsb.queues, we added to the normal queue:
```
RES_REQ = select[type==any] rusage[mem=4000] span[hosts=1] order[slots]
RESRSV_LIMIT = [mem=90000]
MEMLIMIT      = 4000 90000
```
This allows by default jobs to run on a single host and to reserve 4GB of RAM (max 90GB), to kill jobs if they exeed 4GB of RAM (can be changed up to 90GB). Note that reserving memory and setting the limit before LSF kills jobs are two indepent things. So for example if you need 25GB of RAM, add in bsub command: `-R "rusage[mem=25000]" -M 25000`.

To allow the jobs exeeding `MEMLIMIT`  to be killed by LSF, add in /opt/lsf/conf/lsf.conf (see [here](https://www.ibm.com/support/knowledgecenter/#!/SSETD4_9.1.3/lsf_config_ref/lsf.conf.lsb_job_memlimit.5.dita)):
```
LSB_MEMLIMIT_ENFORCE=Y
```



