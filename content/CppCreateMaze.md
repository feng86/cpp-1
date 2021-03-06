# ([C++](Cpp.md)) [CreateMaze](CppCreateMaze.md)

[Maze](CppMaze.md) [code snippet](CppCodeSnippets.md) to create a
square maze. 

[CreateMaze](CppCreateMaze.md) is an improved version of
[CreateMazeSlowly](CppCreateMazeSlowly.md).

 

-   [View a screenshot of 'Maze Creator', showing a generated
    maze](ToolMazeCreator.png).
-   [Go to the page of 'Maze Creator'](ToolMazeCreator.md).

 

 

 

 

 

Project and source code
-----------------------

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.md): [Qt Creator](CppQt.md) 2.0.0

[Project type](CppQtProjectType.md): Qt4 [GUI](CppGui.md) Application

[Compiler](CppCompiler.md): [G++](CppGpp.md) 4.4.1

[Libraries](CppLibrary.md) used:

-   [Qt](CppQt.md): version 4.7.0 (32 bit)
-   [STL](CppStl.md): from [GCC](CppGcc.md), shipped with [Qt
    Creator](CppQt.md) 2.0.0

 

 

 

 

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- //Creates a maze // 0 : path // 1 : wall //From http://www.richelbilderbeek.nl/CppCreateMaze.htm std::vector<std::vector<int> > CreateMaze(const int sz) {   //Assume correct size dimensions   assert( sz > 4 && sz % 4 == 3     && "Size must be 3 + (n * 4) for n > 0");    //Start with a wall-only maze   std::vector<std::vector<int> > maze(sz, std::vector<int>(sz,1));    //Prepare maze, remove paths   // XXXXXXX    1111111   // X X X X    1212121   // XXXXXXX    1111111   // X XOX X -> 1210121   // XXXXXXX    1111111   // X X X X    1212121   // XXXXXXX    1111111    //Draw open spaces   for (int y=1; y<sz; y+=2)   {     for (int x=1; x<sz; x+=2)     {       maze[y][x] = 2; //2: unexplored     }   }    const int mid = sz/2;    maze[mid][mid] = 0;    std::vector<std::pair<int,int> > v;   v.push_back(std::make_pair(mid,mid));   while (!v.empty())   {     //Set a random explorer square at the back     std::swap(v.back(),v[ std::rand() % static_cast<int>(v.size())]);     //Check possible adjacent squares     const int x = v.back().first;     const int y = v.back().second;     std::vector<std::pair<int,int> > next;     if (x > 0 + 2 && maze[y][x-2] == 2) next.push_back(std::make_pair(x-2,y));     if (y > 0 + 2 && maze[y-2][x] == 2) next.push_back(std::make_pair(x,y-2));     if (x < sz - 2 && maze[y][x+2] == 2) next.push_back(std::make_pair(x+2,y));     if (y < sz - 2 && maze[y+2][x] == 2) next.push_back(std::make_pair(x,y+2));     //Dead end?     if (next.empty())     {       v.pop_back();       continue;     }     //Select a random next adjacent square     const int nextIndex = (std::rand() >> 4) % static_cast<int>(next.size());     const int nextX = next[nextIndex].first;     const int nextY = next[nextIndex].second;     //Clear next square     maze[nextY][nextX] = 0;     //Clear path towards next square     maze[(y + nextY)/2][(x + nextX)/2] = 0;     //Add next square to stack     v.push_back(std::make_pair(nextX,nextY));   }   return maze; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

