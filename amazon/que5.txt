// { Driver Code Starts
// Initial Template for C++

#include <bits/stdc++.h>
using namespace std;

 // } Driver Code Ends
// User function Template for C++

class Solution{
    class node{
        public:
        node *next[26];
        bool end;
        node(){
            for(int i=0;i<26;i++){
                next[i]=NULL;
            }
            end=false;
        }
        
    };
    
    class Trie{
        private: node*root;
        public:
        Trie(){
            root=new node();
        }
        void insert(string &s){
            node* it=root;
            for(auto c:s){
                
                if(!it->next[c-'a'])
                it->next[c-'a']=new node();
                
                it=it->next[c-'a'];
            }
            it->end=true;
            
        }
        
        vector<string> find(string &s){
            vector<string>res;
            node*it=root;
            for(auto c:s){
                if(!it->next[c-'a']){
                    res.push_back("0");
                    return res;
                }
                // cout<<c<<endl;
                it=it->next[c-'a'];
            }
            
            // cout<<4434<<endl;
            printall(it,s,res,"");
            
            
            // for(auto c:res){
            //     cout<<s<<c<<" ";
            // }
            // cout<<endl;
            // for(auto c:res)cout<<"ddd"+c<<endl;
            return res;
        }
        void printall(node*it,string &s,vector<string>&res,string cur){
            if(it==NULL){return;}
            if(it->end){
                // cout<<85859<<endl;
                res.push_back(s+cur);}
                for(int i=0;i<26;i++){
                    if(it->next[i]){
                        printall(it->next[i],s,res,cur+char('a'+i));
                    }
                }
            
        }
    };
public:
    vector<vector<string>> displayContacts(int n, string contact[], string s)
    {
        // code here
        Trie t;
        
        for(int i=0;i<n;i++){
            t.insert(contact[i]);
        }
        string q="";
        vector<vector<string>> ans;
        for(int i=0;i<s.size();i++){
            q+=s[i];
            // cout<<q<<endl;
            ans.push_back(t.find(q));
        }
        
        return ans;
    }
};

// { Driver Code Starts.

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        string contact[n], s;
        for(int i = 0;i < n;i++)
            cin>>contact[i];
        cin>>s;
        
        Solution ob;
        vector<vector<string>> ans = ob.displayContacts(n, contact, s);
        for(int i = 0;i < s.size();i++){
            for(auto u: ans[i])
                cout<<u<<" ";
            cout<<"\n";
        }
    }
    return 0;
}  // } Driver Code Ends