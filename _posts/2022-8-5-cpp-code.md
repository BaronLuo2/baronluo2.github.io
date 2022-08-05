---
layout: post
title: "My c++ exhibition"
author: BaronLuo
tags: cpp
---

# My c++ code


```c++

```
## P4544
```c++
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<deque>
using namespace std;
#define ll long long
struct node{
    ll f,x,c;
};
node a[510];
deque <ll> q;
ll n,k,e;
ll dp[510][10010],sum[510];
bool cmp(node a,node b)
{
    return a.x<b.x;
}
int main()
{
    scanf("%lld%lld%lld",&k,&e,&n);
    for(int i=1;i<=n;i++)
    {
        scanf("%lld%lld%lld",&a[i].x,&a[i].f,&a[i].c);
        sum[i]=sum[i-1]+a[i].f;
    }
    memset(dp,0x7f,sizeof(dp));
    sort(a+1,a+n+1,cmp);
    for(ll i=1;i<=n;i++)
    {
        q.clear();
        dp[i-1][0]=0;
        for(int j=0;j<=min(k,sum[i]);j++)
        {
            if(dp[i-1][j]!=0x7f7f7f7f7f7f7f7f)
            {
                while(!q.empty() && dp[i-1][j]-j*a[i].c+j*j*(a[i].x-a[i-1].x)<=dp[i-1][q.back()]-q.back()*a[i].c+q.back()*q.back()*(a[i].x-a[i-1].x))
                {
                    q.pop_back();
                }
                q.push_back(j);
            }
            while(!q.empty() && j-q.front()>a[i].f)
            {
                q.pop_front();
            }
            dp[i][j]=dp[i-1][q.front()]-(ll)q.front()*a[i].c+q.front()*q.front()*(a[i].x-a[i-1].x)+j*a[i].c;
        }
    }
    cout<<dp[n][k]+k*k*(e-a[n].x)<<endl;
    return 0;
}
```

## 3509
```c++
#include<iostream>
#include<cstdio>
using namespace std;
typedef long long ll;
const int maxn=1e6+10;
int n,k,f[maxn],ans[maxn],tmp[maxn];
ll m,a[maxn];
int main()
{
    scanf("%d%d%lld",&n,&k,&m);
    for(int i=1;i<=n;i++)
    {
        scanf("%lld",a[i]);
    }
    int l=1;
    int r=k+1;
    for(int i=1;i<=n;i++)
    {
        while(r+1<=n && a[r+1]-a[i]<a[i]-a[l])
        {
            l++,r++;
        }
        if(a[r]-a[i]>a[i]-a[l])
        {
            f[i]=r;
        }else
        {
            f[i]=l;
        }
    }
    for(int i=1;i<=n;i++)
    {
        a[i]=i;
    }
    while(m)
    {
        if(m&1)
        {
            for(int i=1;i<=n;i++)
            {
                ans[i]=f[ans[i]];
            }
        }
        m=m/2;
        for(int i=1;i<=n;i++)
        {
            tmp[i]=f[i];
        }
        for(int i=1;i<=n;i++)
        {
            f[i]=tmp[f[i]];
        }
    }
    for(int i=1;i<=n;i++)
    {
        printf("%d",ans[i]);
    }
    cout<<endl;
    return 0;
}
```