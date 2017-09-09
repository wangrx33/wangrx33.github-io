---
layout: post
title:  " 中级实训 "
date:   2017-09-09
excerpt: "This term's work is to make a flight which can control by a controller. And creat some new functions to show your ability."
tag:
 - code
 - alpha
 -  operation 
---

##  抛飞 

  抛飞主要通过判断飞机的加速度获取飞机的状态，从而赋予飞机六个电机一个能使其起飞的转速，如1500.根据题目要求，要在不同抛飞力度下上升不同的高度，即根据抛飞时飞机加速度的不同赋予飞机电机不同的转速，从而实现上升不同的高度。


###  code


void FTC_RC::CheckACC(void)   
{	

	if(rc.rawData[THROTTLE] > RC_MINCHECK)
			ftc.f.PaoFei = 0;
			
	if (imu.Acc.length() > ACC_1G)
	{
			if(!ftc.f.PaoFei)
			{
				ftc.f.PaoFei = 1;
			}	
	}
		
		
		if(ftc.f.PaoFei)
			if(imu.Acc.length() > ACC_1G && imu.Acc.length() < ACC_1G * 2.0f )
				Command[THROTTLE] = 1500;
			else if(imu.Acc.length() > ACC_1G * 2.0f && imu.Acc.length() < ACC_1G * 3.0f)
				Command[THROTTLE] = 1700;	
			else
				Command[THROTTLE] = 1900;	
		else
			Command[THROTTLE] = 1350;	
}

