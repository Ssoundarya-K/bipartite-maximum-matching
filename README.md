# bipartite-maximum-matching
M number of cricket players are competing in a Men’s Cricket Tournament’s Auction to get selected by N teams. Each player has a subset of teams that he is interested in. Each team can buy only one more player and each player can be bought by only one team. Find the maximum number of players get selected.

code:
#include <iostream>
using namespace std;
#define M 5
#define N 5
bool graph[M][N];

bool Check_Match(int u, bool seen[], int set[]) {
   for (int v = 0; v < N; v++) { 
      if (graph[u][v] && !seen[v]) { 
         seen[v] = true;  
         if (set[v] < 0 || Check_Match(set[v], seen, set)) {
            set[v] = u; 
            return true;
         }
      }
   }
   return false;
}

int MaxMatch() {
   int set[N];    
   for(int i = 0; i<N; i++)
      set[i] = -1;   
   int count = 0;

   for (int u = 0; u < M; u++) {   
      bool seen[N];
      for(int i = 0; i<N; i++)
         seen[i] = false;    
      if (Check_Match(u, seen, set))   
         count++;
   }
   return count;
}

int main() {
    cout<<"Enter the arrangement of players interest in teams:\n";
    for(int i=0;i<M;i++)
    {
        for(int j=0;j<N;j++)
        {
            cin>>graph[i][j];
        }
    }
    cout << "Maximum number of players who gets selected in teams is: "<< MaxMatch();
    return 0;
}
