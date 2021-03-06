# CS633 Project

## Parallel All Pairs Shortest Path Algorithm

**Team Members:**  
 1. Jatin Dev  
 2. Swapnil Raykar
  
## Directory Structure

-- Parallel-All-Pair-Shortest-Path

    |-- Benchmark
    |   |--readBenchmark.c          // Read the SNAP dataset
    |
    |-- graphGenerator              // Contains the code to genrate the Adjacency Matrix  
    |   |--genAdjacencyMatrix.py
    |
    |-- inputGraphs                 // Store the generated graphs
    |   |-- graph_X	                // The generated graphs wil be stored here(X- no of Vertices)
    |
    |-- profile  
    |   |--profile.*                // Profile files generated by Tau
    |-- Blocked_Parallel.c          // Blocked Parallel Version of APSP
    |-- gen_machinefile.sh          // Generated the machine file with the active nodes
    |-- machinefile                 // These file get generated by gen_machinefile script 
    |-- Makefile                    // Build the 3 source files
    |-- naiveAPSP.c                 // Naive APSP version 
    |-- naiveCheckerboard.c         // Naive CheckerBoard version
    |-- readBinFile.c               // Read Binary input graphs for testing purpose
    |-- README.md                   // ReadMe file
    |-- run.sh                      // Run the Blocked_parallel code on 1024 .. 16384 vertices with 32 .. 256 processes


## Steps to Run the Project  
1. Generate the input graphs using   
    1.1 Random generator  
        ```$ python genAdjacencyMatrix.py <No. of Vertices>```  
        The generated graph gets stored in inputGraphs folder as graph_X  
        
    1.2 Using the Benchmark SNAP(Stanford Network)  
    ```
    $ gcc readBenchmark  
    $ ./a.out <Inputfilename> <NodeCount> <Outputfilename>
    ```  
2. Run the gen_machinefile.sh to generate the machine file  
    ```
    $./gen_machinefile.sh 
    ```

3. Run ``` $make ``` to generate the binaries    

4. Running the 3 versions of APSP  
    3.1 Blocked_Parallel APSP   
    ```
    $ mpiexec -n $P -f machinefile ./Blocked_Parallel.x <Input Graph> <No of Vertices>
    ```
    
    3.2 naive APSP  
    ```
    $ mpiexec -n $P -f machinefile ./naiveAPSP.x <Input Graph> <No of Vertices> 
    /* Here P should be same as < No of Vertices > As we are distibuting 1 vertex to each process */ 
    ```
    
    3.3 naive Checkerboard APSP  
    ```
    $ mpiexec -n 25 -f machinefile ./naiveCheckerboard.x 
    ```
      /* We have fixed the input graph of 5 vertice so we need to use 25 processes */   

4. Use readBinFile.c to test the input graph  
    ```
    $ gcc readBinFile.c
    $ ./a.out <Bin FileName> <No of Vertices>
    ```  

5. Also you can use ```run.sh ``` to run the BlockedParallel verison on 1024..16384 vertices graph with 32..256 processes. 
