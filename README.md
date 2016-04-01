# Floyed-watshal-Algorithm-Graph-Theory-
//This algorithm worked for finding all pair shortest path in a graph.

#include <iostream>
#include <cstdio>
#include <cstdlib>
#include <algorithm>
#include <vector>
#include <cstring>
#define Max 100
using namespace std;

int matrix[Max][Max];
int next[Max][Max];
int Transative_closer[Max][Max];   // Floyed wharshal rule (find the shortest path from every node to all possible nodes )


//find the path
void find_path(int i,int j)
{
    int path;
     path=next[i][j];
     if(path!=j)
     {
           cout << "Node: " <<path << " " ;
          find_path(i,path);
          find_path(path,j);
     }
     return ;
}


int main()
{
        int Node,Edge;
        int i,j,k;

        scanf("%d%d",&Node,&Edge);

         for(i=1;i<=Node;i++)
            for(j=1;j<=Node;j++)
                    {
                       matrix[i][j]=100000000;
                    }

         for(i=1;i<=Node;i++)
            for(j=1;j<=Node;j++)
                    {
                        if(i==j)
                            matrix[i][j]=0;
                    }
        for( i=1;i<=Edge;i++)
        {
          int n1,n2,cost;
          scanf("%d%d%d",&n1,&n2,&cost);
          matrix[n1][n2]=cost;
          next[n1][n2]=n2; // path of each edge
          Transative_closer[n1][n2]=1;
        }



        //main floyed warshal rules
        for(k=1;k<=Node;k++)
        {
            for(i=1;i<=Node;i++)
            {
                for(j=1;j<=Node;j++)
                {

                    if( matrix[i][j] > matrix[i][k] + matrix[k][j])
                        {

                               matrix[i][j] = matrix[i][k] + matrix[k][j];
                               next[i][j]=next[i][k];  // hold the new path
                        }
                }
            }
        }



         // to show the shortest path from each node to node
        for(i=1;i<=Node;i++)
        {
            cout <<"For Node no :" <<i <<endl;
            for(j=1;j<=Node;j++)
            {
                 cout <<"  Node " << j <<" distance " ;
                 cout << matrix[i][j]<<endl;
            }
        }



      // to find the path between the shortest node
        cout << "\n\n\n\nFrom where to where you want to find the path : " <<endl;
        cin >> i>>j;
        cout << "Path from "<< i << " to " << j <<" you must have to touch : " <<endl ;
        find_path(i,j);



       // find the adjacancy of node to node

       for(i=1;i<=Node;i++)
        for(j=1;j<=Node;j++)
            matrix[i][j] = matrix[i][j] || (matrix[i][k] && matrix[k][j]);

          cout << "n\n\n\n\n If you want to search the connection of one node to another node ; then input tow node : "<< endl;
           cin >> i>> j;
            if(Transative_closer[i][j]==1)
                cout << "\n\t Theres a path between " << i<<" and "<<j <<endl ;

    return 0;
}
