/******************************************************************************

                              Online C++ Compiler.
               Code, Compile, Run and Debug C++ program online.
Write your code in this editor and press "Run" button to compile and execute it.

*******************************************************************************/

#include <iostream>
#include<bits/stdc++.h>
using namespace std;
int fibo(int n)
{
    if(n<=1) return n;
    int a = 0;
    int b = 1;
    int fib;
    for(int i=2;i<=n;i++)
    {
        fib = a+b;
        a= b;
        b = fib;
    }
    return fib;
}
int fibor(int n)
{
    if(n<=1) return n;
    return fibor(n-1)+fibor(n-2);
}
bool safe(int row,int col,int n,vector<string> &board)
{
    int nr = row;
    int nc = col;
    while(nc>=0)
    {
        if(board[nr][nc]=='Q') return false;
        nc--;
    }
    nc = col;
    while(nr>=0 && nc>=0)
    {
        if(board[nr][nc]=='Q') return false;
        nr--;
        nc--;
    }
    nr = row;
    nc = col;
    while(nr<n && nc>=0)
    {
        if(board[nr][nc]=='Q') return false;
        nr++;
        nc--;
    }
    return true;
}
void nqueen(int col,int n,vector<string> &board,vector<vector<string>> &boards)
{
    if(col==n)
    {
        boards.push_back(board);
        return;
    }
    for(int row = 0;row<n;row++)
    {
        if(safe(row,col,n,board))
        {
            board[row][col] = 'Q';
            nqueen(col+1,n,board,boards);
            board[row][col] = '.';
        }
    }
}
int part(vector<int>& arr,int low,int high)
{
    int pivot = arr[high];
    int i = low-1;
    for(int j = low;j<high;j++)
    {
        if(arr[j]<=pivot)
        {
            i++;
            swap(arr[i],arr[j]);
        }
    }
    swap(arr[i+1],arr[high]);
    return i+1;
}
void quickSort(vector<int>& arr,int low,int high)
{
    if(low<high)
    {
        int pi = part(arr,low,high);
        quickSort(arr,low,pi-1);
        quickSort(arr,pi+1,high);
    }
}
int knapSack(int ind,int w,vector<int> &wt,vector<int> &val,vector<vector<int>> &dp)
{
    if(ind==0)
    {
        if(wt[0]<=w) return val[0];
        return 0;
    }
    if(dp[ind][w]!=-1) return dp[ind][w];
    int nt = knapSack(ind-1,w,wt,val,dp);
    int take= INT_MIN;
    if(wt[ind]<=w){
        take = val[ind] + knapSack(ind-1,w-wt[ind],wt,val,dp);
    }
    return dp[ind][w] = max(nt,take);
}

struct Node{
  int freq;
  char ch;
  Node* left;
  Node* right;
  Node(char chh,int freqq)
  {
      freq = freqq;
      ch = chh;
      left = right = nullptr;
  }
};
struct compare{
  bool operator()(Node* a,Node* b)
  {
      return a->freq > b->freq;
  }
};
void printCodes(Node* root,string s)
{
    if(!root) return;
    if(root->ch!='$')
        cout<<root->ch<<" : "<<s<<endl;
    printCodes(root->left,s+"0");
    printCodes(root->right,s+"1");
}
void huffMan(vector<char>& chs,vector<int>& freqs)
{
    int n = freqs.size();
    priority_queue<Node*,vector<Node*>,compare> pq;
    for(int i=0;i<n;i++)
    {
        pq.push(new Node(chs[i],freqs[i]));
    }
    
    while(pq.size()>1)
    {
        Node* left = pq.top();
        pq.pop();
        Node* right = pq.top();
        pq.pop();
        Node* top = new Node('$',left->freq+right->freq);
        top->left = left;
        top->right = right;
        pq.push(top);
    }
    
    printCodes(pq.top(),"");
}
int main()
{
    std::cout<<"Hello World";
    int n = 4;
    cout<<fibo(n);
    cout<<endl<<fibor(n)<<endl;
    vector<vector<string>> boards;
    vector<string> board(n,string(n,'.'));
    nqueen(0,n,board,boards);
    for(auto i : boards)
    {
        for(auto j : i){
            cout<<j<<endl;;
        }
        cout<<"------------------\n";
    }
    vector<int> arr = {4,2,5,1,3};
    quickSort(arr,0,4);
    for(auto i : arr){
        cout<<i<<" ";
    }
    cout<<endl;
    
    vector<int> wt = {2,3,4};
    vector<int> val = {20,30,40};
    int w = 5;
    vector<vector<int>> dp(3,vector<int>(w+1,-1));
    cout<<"------------------------\n"<<knapSack(2,w,wt,val,dp)<<endl;
    
    
    
    vector<char> chs = {'a','b','c','d','e','f'};
    vector<int> freqs = {5,9,12,13,16,45};
    huffMan(chs,freqs);
    
    
    
    return 0;
}
