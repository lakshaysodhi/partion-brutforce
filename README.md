# partion-brutforce
HIRINGWO codechef
#include <bits/stdc++.h>
using namespace std;
#define ull unsigned long long
#define ll long long
#define ld long double
#define MOD (pow(10,9)+7)
int sum(vector<int> &A){
           int sum=0;
           for(int i=0;i<A.size();i++){
                     sum+=A[i]; 
           }
           return sum;
}
int bruteforce(vector<int> A,int k){
           int ans=INT_MAX;
           if(k==A.size()){
                      return sum(A);
           }
           
           for(int i=0;i<A.size();i++){
           
                      for(int j=i+1;j<A.size();j++){
                                 vector<int> temp;
                                 temp.push_back(A[i]*A[j]);
                                 for(int k=0;k<A.size();k++){
                                            if(k!=i && k!=j){
                                                       temp.push_back(A[k]);
                                            }
                                 }
                                 ans=min(ans,bruteforce(temp,k));
                      }
                      
           }
           
           return ans;
}

int main()
{
           int t;
           cin>>t;
           while(t--){
                      int k,x;
                      cin>>k>>x;
                      unordered_map<int,int> prime;
                      int count=0;
                      
                      while(x%2==0){
                                 count++;
                                 x=x/2;
                      }
                      prime[2]=count;
                      
                      for(int i=3;x!=1;i=i+2){
                                 count=0;
                                 while(x%i==0){
                                         count++;
                                         x=x/i;
                                 }
                                 if(count>0)
                                 prime[i]=count;
                      }
                      int sum=0;
                      if(prime.size()==k){
                                 
                                 for(auto i=prime.begin();i!=prime.end();i++){
                                          sum+=pow(i->first,i->second);  
                                 }
                      }else if(prime.size()<k){
                               
                                 for(auto i=prime.begin();i!=prime.end();i++){
                                          sum+=pow(i->first,i->second);  
                                 }
                                 sum+=(k-prime.size());
                      }else{
                                 vector<int> A(prime.size());
                                 int x=0;
                                 for(auto i=prime.begin();i!=prime.end();i++){
                                          A[x++]=pow(i->first,i->second);  
                                 }
                                 sum=bruteforce(A,k);
                                 
                      }
                      cout<<sum<<endl;
           }
               
}

