Download Link: https://assignmentchef.com/product/solved-csci-4320-6360-assignment-1
<br>
HighLife Using 1-D Arrays

To prepare you for upcoming programming assignments in CUDA, you are to construct a C program that specifically implements a modification to Conway’s Game of Life called HighLife but with the additional twist of using ***only*** 1-D arrays. Additionally, you will run this C-program on the AiMOS supercomputer at the CCI in serial mode. This will prepare you for the batch queuing system of CCI computing resources.1.1 HighLife SpecificationThe HighLife is an example of a Cellular Automata where universe is a two-dimensional orthogonal grid of square cells (with WRAP AROUND FOR THIS ASSIGNMENT), each of which is in one of two possible states, ALIVE or DEAD. Every cell interacts with its eight neighbors, which are the cells that are horizontally, vertically, or diagonally adjacent. At each step in time, the following transitions occur at each and every cell:• Any LIVE cell with FEWER THAN two (2) LIVE neighbors DIES, as if caused by under-population.• Any LIVE cell with two (2) OR three (3) LIVE neighbors LIVES on to the next generation.• Any LIVE cell with MORE THAN three (3) LIVE neighbors DIES, as if by over-population.• Any DEAD cell with EXACTLY three (3) or six (6) LIVE neighbors becomes a LIVE cell, as if by reproduction/birth.

The world size and initial pattern are determined by an arguments to your program. A template for your program will be provide and more details are below. The first generation is created by applying the above rules to every cell in the seed—births and deaths occur simultaneously, and the discrete moment at which this happens is sometimes called a “tick” or iteration. The rules continue to be applied repeatedly to create further generations. The number of generations will also be an argument to your program. Note, an iteration starts with Cell(0, 0) and ends with Cell(N – 1, N – 1) in the serial case.1.2 Template and Implementation DetailsFor the provided template, highlife.c, there are the following functions you must write.• HL swap: this function will perform the swap operation of the two pointers.• HL countAliveCells: this function check each of the 8 neighbors and counts the alive cells. Note, you will have to access the data array by performing you own pointer math using the x0, x1, x2, y0, y1 and y2 arguments.• HL iterateSerial: this function takes as an argument the number of iterations and compute the world and swaps the new world with the previous world to be ready for next iteration. There are for-loops already defined. You need to fill in the code in the for-loops.Please do not change the data structures or function call signatures. Additionally, all the header files you need for this assignment are already included.To compile and execute the HighLife program, do:• compile: make all – this will invoke the GCC compiler with debug and all warnings turned on.• run: ./highlife 4 32 2 – this will execute the HighLife program using pattern 4 for a world size of 32×32 and perform two iterations. Pattern 4 is a “spinner” pattern that is at the corners of the grid. For this assignment, all world sizes will be 32×32.For this assignment, there are the following 6 patterns:• Pattern 0: World is ALL zeros.• Pattern 1: World is ALL ones.• Pattern 2: Streak of 10 ones in about the middle of the World.• Pattern 3: Ones at the corners of the World.• Pattern 4: “Spinner” pattern at corners of the World.• Pattern 5: 3-generation predecessor of the replicator.For help in seeing how various patterns should evolve, please see: https://www.conwaylife. com/wiki/OCA:HighLife

1.3 Helper InformationTo aide you the development of the above functions and 2-D array indexing using only a 1-D array data structure, please use the following algorithmic help.First, if you had a 2-D array structures, and you wish to know if data[x1][y1] is alive or dead, you would need to know the status of cells data[x1-1][y1-1], data[x1+1][y1-1],data[x1+1][y1-1], data[x1-1][y1], data[x1+1][y1], data[x1-1][y1], data[x1-1][y1+1], data[x1][y1+1] and data[x1+1][y1+1]. However, we need to access to be for a 1-D array. So, let’s compute the pointer address offsets need. First, we want data[x1][y1] to become data[x1 + y1] and we need to determine what x0 (e.g., &amp;data[x1 -1]) and x2 or &amp;data[x1+ 1] will be as well as y0, y2 will be be. Also, we need to account for the factor that the 2-d world has wrap-around. For this, the x and y pointer offsets become:y0 = ((y + g_worldHeight – 1) °h g_worldHeight) * g_worldWidth;y1 = y * g_worldWidth;y2 = ((y + 1) °h g_worldHeight) * g_worldWidth;And for an x values over the range of 0 to g worldWidth-1:x1 = xx0 = (x1 + g_worldWidth – 1) °h g_worldWidth;x2 = (x1 + 1) °h g_worldWidth;2 Running on AiMOSIn addition to giving students experience with C-programming (coming from say C++) an additional goal of the assignment is for students to gain experience in running a jobs on the AiMOS supercomputer. While you are allowed to develop your highlife program on any Linux platform, you should run it on AiMOS and verify it works there prior to making your final submission. Note that submitty.cs.rpi.edu will compile and test your code’s automatically and no run data from AiMOS is required for this assignment.To execute on AiMOS, please follow the steps below:1. Login to CCI landing pad (blp[01..04].ccni.rpi.edu) using SSH and your CCI account, PIC, Google Authenticator token and password information. Google Authen¬ticator can be found at: https://apps.apple.com/us/app/google-authenticator/ id388497605 for Apple iPhone and at https://play.google.com/store/apps/details? id=com.google.android.apps.authenticator2&amp;hl=en_US&amp;gl=US for Android phones. See the CCI documentation for how to setup your password, PIC and Two-factor au¬thentication, here: https://secure.cci.rpi.edu/wiki/accounts/user_accounts/2. Login to AiMOS front end by doing ssh <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="d9899a89e8e9a0b6acabb5b6beb0b799bdbaaabfbcb7e9e8f7">[email protected]</a>3. (Do one item only). Setup ssh-keys for passwordless login between compute nodes via ssh-keygen -t rsa and then cp /.ssh/id rsa.pub /.ssh/authorized keys.4. Load modules: run the module load gcc command. This puts the GNU C compiler in your path correctly as well as all needed libraries, etc.

5. Compile code on front end by issuing the make command.6. Get a single node allocation by issuing: salloc -N 1 -t 30 which will allocate a single compute node for 30 mins. The max time for the class is 30 mins per job. Your salloc command will return once you’ve been granted a node. Normally, it’s been immediate but if the system is full of jobs you may have to wait for some period of time.7. Use the squeue to find the dcsXYZ node name (e.g., dcs24).8. SSH to that compute node, for example, ssh dcs24. You should be at a Linux prompt on that compute node.9. Issue run command for GOL. For example, ./highlife 4 32 2 which will run GOL using pattern 4 with a world size of 32×32 for 2 iterations.10. If you are done with a node early, please exit the node and cancel the job with scancel JOBID where the JOBID can be found using the squeue command.3 HAND-IN and GRADING INSTRUCTIONSPlease submit your C-code to the submitty.cs.rpi.edu grading system. The grading rubric will be available to test your solution. Please make sure you document the code you write for this assignment. That is, say what you are doing and why.