#include<stdio.h> 
 
int main() 
{ 
 
  int num,j,n,time,remain,flag=0,time_qtm; 
  int wait_time=0,turnaround_time=0,at[10],bt[10],rt[10]; 
  printf("Enter Total Process:\t "); 
  scanf("%d",&n); 
  remain=n; 
  for(num=0;num<n;num++) 
  { 
    printf("Enter Arrival and Burst Time for Process %d :",num+1); 
    scanf("%d",&at[num]); 
    scanf("%d",&bt[num]); 
    rt[num]=bt[num]; 
  } 
  printf("Enter Time Quantum:\t"); 
  scanf("%d",&time_qtm); 
  printf("\n\nProcess\t|Turnaround Time|\tWaiting Time\n\n"); 
  for(time=0,num=0;remain!=0;) 
  { 
    if(rt[num]<=time_qtm && rt[num]>0) 
    { 
      time+=rt[num]; 
      rt[num]=0; 
      flag=1; 
    } 
    else if(rt[num]>0) 
    { 
      rt[num]-=time_qtm; 
      time+=time_qtm; 
    } 
    if(rt[num]==0 && flag==1) 
    { 
      remain--; 
      printf("P[%d]\t|\t%d\t|\t%d\n",num+1,time-at[num],time-at[num]-bt[num]); 
      wait_time+=time-at[num]-bt[num]; 
      turnaround_time+=time-at[num]; 
      flag=0; 
    } 
    if(num==n-1) 
      num=0; 
    else if(at[num+1]<=time) 
      num++; 
    else 
      num=0; 
  } 
  printf("\nAverage Waiting Time= %f\n",wait_time*1.0/n); 
  printf("Avg Turnaround Time = %f",turnaround_time*1.0/n); 
  
  return 0; 
}
