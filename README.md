# osproject
#include<stdio.h>
#include<stdlib.h>

int main()
{
int n,i,j;
int p,q,r,x=0;
int var=0;
printf("---------------LET'S  START-------------------\n\n");

printf("ENTER NUMBER OF PROCESSES = ");
scanf("%d",&n);
int qu1[n],qu2[n],qu3[n];
int priority[n],process[n],btime[n],atime[n],rtime[n];

for(i=0;i<n;i++)
{
printf("\nENTER PROCESS NAME FOR PROCESS %d = ",i+1,"\n");
printf("PROCESS ");
scanf("%d",&process[i]);
printf("enter priority = ");
scanf("%d",&priority[i]);
printf("enter burst time = ");
scanf("%d",&btime[i]);
}
for(i=0;i<n-1;i++)
{
for(j=0;j<(n-i-1);j++)
{
if(priority[j]>priority[j+1])
{
	//sorting of process according to its priorities
var=priority[j];
priority[j]=priority[j+1];
priority[j+1]=var;

var=process[j];
process[j]=process[j+1];
process[j+1]=var;

var=btime[j];
btime[j]=btime[j+1];
btime[j+1]=var;
}
}
}
printf("\n\n");
printf("process     priority      burst time\n");
for(i=0;i<n;i++)
{
printf("P%d",process[i]);
printf("            %d",priority[i]);
printf("            %d",btime[i]);
printf("\n");
}
printf("\nENTER NUMBER OF PROCESSES TO SEND IN QUEUE 1 =");
scanf("%d",&p);
printf("ENTER NUMBER OF PROCESSES TO SEND IN QUEUE 2 =");
scanf("%d",&q);
printf("ENTER NUMBER OF PROCESSES TO SEND IN QUEUE 3 =");
scanf("%d",&r);
for(i=0;i<p;i++)
{
qu1[x]=priority[i];
x=x+1;
}

printf("\n");
printf("\n1)--------------------QUEUE 1-----------------------");
printf("\n\n");
printf(" _____________________________________________________\n");
printf("|	QUEUE 1            |        PRIORITY	      |   \n");
printf("|__________________________|__________________________|\n");
for(i=0;i<p;i++){
printf("|	  P%d		   ",process[i]);
printf("|          %d               |\n",priority[i]);
}
printf("|__________________________|__________________________|\n\n");
for(i=p;i<p+q;i++){
qu2[x]=priority[i];
x=x+1;
}
printf("\n");
printf("\n2)----------------------QUEUE 2-----------------------");
printf("\n\n");
printf(" ____________________________________________________\n");
printf("|	QUEUE 2            |    PRIORITY	     | \n");
printf("|__________________________|_________________________|\n");
for(i=p;i<p+q;i++){
printf("|	  P%d		   ",process[i]);
printf("|          %d              |\n",priority[i]);
}
printf("|__________________________|_________________________|\n\n");
for(i=p+q;i<p+q+r;i++){
qu3[x]=priority[i];
x=x+1;
}
printf("\n");
printf("\n3)---------------------QUEUE 3---------------------");
printf("\n\n");
printf(" ____________________________________________________\n");
printf("| QUEUE 3	           |       PRIORITY	    | \n");
printf("|__________________________|________________________|\n");
for(i=p+q;i<p+q+r;i++){
printf("|	  P%d		   ",process[i]);
printf("|          %d             |\n",priority[i]);
}
printf("|__________________________|________________________|\n");
printf("\n");
while(true)
{
int ch;
printf("\n\npress 1 for round robin\n2 for priority scheduling\n3 for first come first serve\n4 to execute all at once\n5 to exit\n");
scanf("%d",&ch);
	int tq,t,remain,flag=0;
float waiting_time=0,turn_time=0;
int wt[n],tat[n]; 
float avwtime=0,avtatime=0;

int total=0;
int wtime[n],ttime[n];
float avg_wtime,avg_tatime;
switch(ch)
{

	case 1:

remain=p;
printf("\n\n----------ROUND ROBIN SCHEDULING FOR QUEUE 1----------\n\n");
for(i=0;i<p;i++){
printf("ENTER ARRIVAL TIME Process%d =",process[i]);
scanf("%d",&atime[i]);
rtime[i]=btime[i];
}
printf("enter time quantum = ");
scanf("%d",&tq);
printf("_______________________________________________");
printf("\n|Process |  Turnaround time |  Waiting time    |\n");
printf("|________|__________________|__________________|\n");
for(t=0,i=0;remain!=0;)
{
if(rtime[i]<=tq && rtime[i]>0)
{
t=t+rtime[i];
rtime[i]=0;
flag=1;
}
else if(rtime[i]>0)
{
rtime[i]=rtime[i]-tq;
t=t+tq;
}
if(rtime[i]==0 && flag==1)
{
remain--;
printf("|P%d      |         %d        |       %d          | \n",i+1,t-atime[i],t-atime[i]-btime[i]);
printf("|________|__________________|__________________|\n");
waiting_time=waiting_time+t-atime[i]-btime[i];
turn_time=turn_time+t-atime[i];
flag=0;
}
if(i==p-1)
i=0;
else if(atime[i+1]<=t)
i++;
else
i=0;
}
printf("\nAverage waiting time= %f\n",waiting_time/p);
printf("Average turnaround time= %f\n",turn_time/p);
break;

case 2:
printf("\n\n\n----------PRIORITY QUEUE SCHEDULING FOR QUEUE 2----------\n\n");

wtime[p]=0;
for(i=p+1;i<p+q;i++){
wtime[i]=0;
for(j=p;j<i;j++)
wtime[i]=wtime[i]+btime[j];
total=total+wtime[i];
}
avg_wtime=total*1.0/q;
total=0;
printf("_______________________________________________");
printf("\n|Process |  Turnaround time |  Waiting time    |\n");
printf("|________|__________________|__________________|\n");
for(i=p;i<p+q;i++)
{
ttime[i]=btime[i]+wtime[i];
total=total+ttime[i];
printf("|P%d      |         %d        |       %d          | \n",i+1,btime[i],wtime[i],ttime[i]);
printf("|________|__________________|__________________|\n");
}
avg_tatime=total/q;
printf("\nAverage waiting time= %f\n",avg_wtime);
printf("Average turnaround time= %f\n",avg_tatime);
break;

case 3:
printf("\n\n\n----------FIRST COME FIRST SERVE (FCFS) SCHEDULING FOR QUEUE 3----------\n\n");

wt[p+q]=0;
for(i=p+q+1;i<p+q+r;i++)
{
wt[i]=0;
for(j=p+q;j<i;j++)
wt[i]=wt[i]+btime[j];
}
printf("_______________________________________________");
printf("\n|Process |  Turnaround time |  Waiting time    |\n");
printf("|________|__________________|__________________|\n");
for(i=p+q;i<p+q+r;i++)
{
tat[i]=btime[i]+wt[i];
avwtime=avwtime+wt[i];
avtatime=avtatime+tat[i];
printf("|P%d      |         %d        |       %d          | \n",i+1,btime[i],wt[i],tat[i]);
printf("|________|__________________|__________________|\n");
}

printf("\nAverage waiting time= %f\n",avwtime/r);
printf("Average turnaround time= %f\n",avtatime/r);
break;

case 4:
remain=p;
printf("\n\n----------ROUND ROBIN SCHEDULING FOR QUEUE 1----------\n\n");
for(i=0;i<p;i++){
printf("ENTER ARRIVAL TIME Process%d =",process[i]);
scanf("%d",&atime[i]);
rtime[i]=btime[i];
}
printf("enter time quantum = ");
scanf("%d",&tq);
printf("_______________________________________________");
printf("\n|Process |  Turnaround time |  Waiting time    |\n");
printf("|________|__________________|__________________|\n");
for(t=0,i=0;remain!=0;)
{
if(rtime[i]<=tq && rtime[i]>0)
{
t=t+rtime[i];
rtime[i]=0;
flag=1;
}
else if(rtime[i]>0)
{
rtime[i]=rtime[i]-tq;
t=t+tq;
}
if(rtime[i]==0 && flag==1)
{
remain--;
printf("|P%d      |         %d        |       %d          | \n",i+1,t-atime[i],t-atime[i]-btime[i]);
printf("|________|__________________|__________________|\n");
waiting_time=waiting_time+t-atime[i]-btime[i];
turn_time=turn_time+t-atime[i];
flag=0;
}
if(i==p-1)
i=0;
else if(atime[i+1]<=t)
i++;
else
i=0;
}
printf("\nAverage waiting time= %f\n",waiting_time/p);
printf("\nAverage turnaround time= %f\n",turn_time/p);

printf("\n\n\n----------PRIORITY QUEUE SCHEDULING FOR QUEUE 2----------\n\n");

wtime[p]=0;
for(i=p+1;i<p+q;i++){
wtime[i]=0;
for(j=p;j<i;j++)
wtime[i]=wtime[i]+btime[j];
total=total+wtime[i];
}
avg_wtime=total/p;

printf("_______________________________________________");
printf("\n|Process |  Turnaround time |  Waiting time    |\n");
printf("|________|__________________|__________________|\n");
for(i=p;i<p+q;i++)
{
ttime[i]=btime[i]+wtime[i];
total=total+ttime[i];
printf("|P%d      |         %d        |       %d          | \n",i+1,btime[i],wtime[i],ttime[i]);
printf("|________|__________________|__________________|\n");
}
avg_tatime=total/q;
printf("\nAverage waiting time= %f\n",avg_wtime);
printf("Average turnaround time= %f\n",avg_tatime);

printf("\n\n\n----------FIRST COME FIRST SERVE (FCFS) SCHEDULING FOR QUEUE 3----------\n\n");

wt[p+q]=0;
for(i=p+q+1;i<p+q+r;i++)
{
wt[i]=0;
for(j=p+q;j<i;j++)
wt[i]=wt[i]+btime[j];
}
printf("_______________________________________________");
printf("\n|Process |  Turnaround time |  Waiting time    |\n");
printf("|________|__________________|__________________|\n");
for(i=p+q;i<p+q+r;i++)
{
tat[i]=btime[i]+wt[i];
avwtime=avwtime+wt[i];
avtatime=avtatime+tat[i];
printf("|P%d      |         %d        |       %d          | \n",i+1,btime[i],wt[i],tat[i]);
printf("|________|__________________|__________________|\n");
}

printf("\nAverage waiting time= %f\n",avwtime/r);
printf("Average turnaround time= %f\n",avtatime/r);

break;

case 5:exit(0);
}
}
}
