# 12945-Magicka-Spell

#include <stdio.h>
#include<string.h>
#include <stdbool.h>
#include <stdlib.h>
char s[101][51];
int flag[101];
int l[101];
char ans[101][51];

void bubblesort (char *ap, int n) {
      char temp;
      for (int i = 0; i < n-1; i++) {
            for (int j = 0; j < n-1-i; j++) {
                  if (ap[j] < ap[j + 1]) {
                       temp = ap[j];
                       ap[j] = ap[j + 1];
                       ap[j + 1] = temp;
                  }
            }
      }
}

void bubblesort1 (char *ap,char *ap2, int n,int n1) {
    if (n < n1) {
        swap(ap,ap2);
    }
}
void swap(char* a,char* b)
{
    int l1=strlen(a);
    int l2=strlen(b);
    int flag=0;
    if(l1>l2)flag=1;
    if(l1<l2)flag=0;
    if(l1==l2)flag=2;
    char tmp[51];
    for(int i=0;i<l1;i++)tmp[i]=a[i];
    for(int i=0;i<l2;i++){
        a[i]=b[i];
    }
    for(int i=0;i<l1;i++){
        b[i]=tmp[i];
    }
    if(flag==1){
        for(int i=l2;i<l1;i++)
            a[i]='\0';
    }
    if(flag==0){
        for(int i=l1;i<l2;i++)
            b[i]='\0';
    }
}

int main()
{
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++)scanf("%s",s[i]);
    for(int i=0;i<n;i++){
        l[i]=strlen(s[i]);
        bubblesort(s[i],l[i]);
        flag[i]=1;
    }
    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            bubblesort1(s[i],s[j],strlen(s[i]),strlen(s[j]));
        }
    }
    for(int i=0;i<n;i++){
        l[i]=strlen(s[i]);
        //printf("!!%s\n",s[i]);
    }
    for(int i=0;i<n;i++){
        strcpy(ans[i],s[i]);
        for(int j=i+1;j<n;j++){
            if(l[i]>l[j])strcpy(ans[i],s[i]);
            if(l[i]==l[j]){
                if(strcmp(s[i],s[j])>0){
                    strcpy(ans[i],s[i]);
                }
                if(strcmp(s[i],s[j])==0){
                    strcpy(ans[i],s[i]);
                }
                if(strcmp(s[i],s[j])<0){
                    swap(s[i],s[j]);
                    strcpy(ans[i],s[i]);
                }
            }
        }
    }
    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if(strcmp(ans[i],ans[j])==0)
                flag[j]=0;
        }
        //printf("%d:%d\n",i,flag[i]);
    }
    for(int i=0;i<n;i++){
        if(flag[i]!=0)
            printf("%s\n",ans[i]);
    }
}
