---
layout: post
title:  "How to clean up some running jobs on a linux cluster- example"
date:   2015-02-17 15:19:01
categories: Systems
published: true
comments: true
---
#How to how-to-cleanup-fluent-hammer22:


	#!/bin/sh

	# This file was generated by FLUENT.  To kill FLUENT and all its
	# related processes, run this script.  If
	# FLUENT exits normally, this file will be removed automatically.


	if [ `/bin/uname` = HP-UX ]; then
	REMOTE_SH=remsh
	else
		REMOTE_SH=rsh
	fi

	KILL_CMD="kill -9 "
	LOCALHOST=`hostname`
	if [ $LOCALHOST = hammer22 ]; then $KILL_CMD 3260; else $REMOTE_SH hammer22 $KILL_CMD 3260; fi
	if [ $LOCALHOST = hammer22.rcc.psu.edu ]; then 		$KILL_CMD 3151; else $REMOTE_SH hammer22.rcc.psu.edu $KILL_CMD 3151; fi
	/bin/rm -f /gpfs/home/hup128/cleanup-fluent-hammer22.rcc.psu.edu-3151.sh


I also for a while have been getting the traffic on our LionX machine for getting the stats and do some visuallization on the data. This the script that export the data, I will later drop the visuallization platform that aimed to list the resutls. 

	#!/bin/bash
Eevery one hour get the load balance off the system every 30 min

	START= `date +%s`
	while [ $(( $(date +%s) - 30))-lt $START ]; do
	./system_data_download.txt
	sleep 30
	done




	#!/bin/bash
	now=$(date +"%m_%d_%Y   %H_%M")
	cd ~/scratch/lionxg
	touch Qdata_sys_lionxg.txt
	qstat -q > Qdata_sys_lionxg.txt
	echo "Starting system load information at _$now" | cat - Qdata_sys_lionxg.txt >> Qdata_sys_lionxg_full.txt



	#for unlisted qstat
	touch Udata_sys_lionxg.txt
	qstat  > Udata_sys_lionxg.txt
	echo "Starting system load information at _$now" | cat - Udata_sys_lionxg.txt >> Udata_sys_lionxg_full.txt


	#for full attributes, qstat
	touch Fulldata_sys_lionxg.txt
	qstat -f > Fulldata_sys_lionxg.txt
	echo "Starting system load information at _$now" | cat - Fulldata_sys_lionxg.txt >> Fulldata_sys_lionxg_full.txt