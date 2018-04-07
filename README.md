# osproject
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
int main()
{
int n,i,j,a,b,c,x=0,temp=0;
printf("enter number of process\n");
scanf("%d",&n);
int qu1[n],qu2[n],qu3[n],priority[n],process[n],btime[n],atime[n];

for(i=0;i<n;i++)
{
printf("enter process %d= ",i+1,"\n process");
scanf("%d= ",&process[i]);
printf("enter burst time for this process");
scanf("%d= ",&btime[i] );
printf("enter priority for this process");
scanf("%d = ",&priority[i]);
}
for(i=0;i<n-1;i++)
{
for(j=0;j<(n-i-1);j++)
{
if(priority[j]>priority[j+1])
{
temp=priority[j];
priority[j]=priority[j+1];
priority[j+1]=temp;

temp=process[j];
process[j]=process[j+1];
process[j+1]=temp;

temp=btime[j];
btime[j]=btime[j+1];
btime[j+1]=temp;
}
}
}
printf("\n\n");
for(i=0;i<n;i++)
{
printf("Process P%d",process[i]);
printf(" with priority %d",priority[i]);
printf("has burst time %d",btime[i]);
printf("\n");
}
printf("\nENTER NUMBER OF PROCESSES TO SEND IN QUEUE 1 =");
scanf("%d",&a);
printf("ENTER NUMBER OF PROCESSES TO SEND IN QUEUE 2 =");
scanf("%d",&b);
}
