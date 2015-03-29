#include<bits/stdc++.h>
using namespace std;
const int N=50005,M=500005;
int n,m,D,Ans[M],L[M],R[M],Mx[M],k[M],ww;

struct Po
{vector<int> W,K;
 int d[2],mx[2],mn[2],id;
 Po *l,*r;
 Po(int x=0,int y=0,int i=0){d[0]=mx[0]=mn[0]=x;d[1]=mx[1]=mn[1]=y;id=i;}
 int& operator[](int i){return d[i];}
 void up(Po *x)
 {if(!x) return;
  for(int i=0;i<2;i++) mx[i]=max(mx[i],x->mx[i]),mn[i]=min(mn[i],x->mn[i]);
 }
 void up(){up(l);up(r);}
}p[M],*root,Ap[N];

bool operator<(Po A,Po B){return A[D]<B[D];}

#define Mid (l+r>>1)
Po* Bu(int l,int r,int Now)
{if(l>r) return 0;
 D=Now;nth_element(p+l,p+Mid,p+r+1);
 Po *x=p+Mid;
 return x->l=Bu(l,Mid-1,Now^1),x->r=Bu(Mid+1,r,Now^1),x->up(),x;
}

bool ok(Po *x,Po p)
{if(!x) return 0;
 if(x->mn[0]<p[0]&&x->mn[1]<p[0]) return 1;
 if(x->mx[0]>p[1]&&x->mx[1]>p[1]) return 1;
 return 0;
}

void Ask(Po *x,Po Ap,int k)
{if(!x) return;
 if(x->mx[0]<Ap[0]&&x->mx[1]<Ap[0]||x->mn[0]>Ap[1]&&x->mn[1]>Ap[1]) return x->W.push_back(k);
 if(x->d[0]<Ap[0]&&x->d[1]<Ap[0]||x->d[0]>Ap[1]&&x->d[1]>Ap[1]) x->K.push_back(k);
 if(ok(x->l,Ap)) Ask(x->l,Ap,k);
 if(ok(x->r,Ap)) Ask(x->r,Ap,k);
}

#define Lc (x<<1)
#define Rc (x<<1|1)
#define Mid (l+r>>1)

void up(int x,int l,int r)
{if(x)
 {L[x]=L[Lc];R[x]=R[Rc];Mx[x]=max(Mx[Lc],max(Mx[Rc],R[Lc]+L[Rc]));
  if(L[Lc]==Mid-l+1) L[x]+=L[Rc];
  if(R[Rc]==r-Mid) R[x]+=R[Lc];
 }
}

void Bud(int x,int l,int r)
{L[x]=R[x]=Mx[x]=r-l+1;
 if(l!=r) Bud(Lc,l,Mid),Bud(Rc,Mid+1,r);
}

void Xor(int x,int l,int r,int p)
{if(l==r)
 {k[x]^=1;
  if(k[x]) L[x]=R[x]=Mx[x]=0;
  else L[x]=R[x]=Mx[x]=1;
 }
 else
 {if(p<=Mid) Xor(Lc,l,Mid,p);
  else Xor(Rc,Mid+1,r,p);
  up(x,l,r);
 }
}

void Work(Po *x)
{if(!x) return;
 for(int i=0;i<x->W.size();i++) Xor(1,1,n,x->W[i]);
 for(int i=0;i<x->K.size();i++) Xor(1,1,n,x->K[i]);
 Ans[x->id]=Mx[1];
 for(int i=0;i<x->K.size();i++) Xor(1,1,n,x->K[i]);
 Work(x->l);Work(x->r);
 for(int i=0;i<x->W.size();i++) Xor(1,1,n,x->W[i]);
}

int main()
{freopen("2378.in","r",stdin);
 freopen("2378.out","w",stdout);
 scanf("%d%d",&n,&m);
 for(int i=1;i<=n;i++) scanf("%d%d",&Ap[i][0],&Ap[i][1]);
 for(int i=1,x,y;i<=m;i++) scanf("%d%d",&x,&y),p[i]=Po(x,y,i);
 root=Bu(1,m,0);
 for(int i=1;i<=n;i++) Ask(root,Ap[i],i);
 cout<<ww<<endl;Bud(1,1,n);Work(root);
 for(int i=1;i<=m;i++) printf("%d\n",Ans[i]);
 return 0;
}
