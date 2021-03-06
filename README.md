Dice game:

This program is a game that has 3 players that uses fifos, parent and child processes, signals, and file descriptors.

The game will generate a random number betwween 0 and 6 for each player up until the total of a players points rolled is 40.
The referee of the gae will be getting signals from the 3 different players to depict when each player rolls and how many points they will gain.

main: the main method declares the process id's for 3 different players, 4 file descriptors will be made for player2, and 2 fifo's for player3. The program will fork a process id in doing that it will duplicate a process and call the player 1 function. It will then for the pid2 variable to create another process for player 2 and we call file descriptor 3 and 4  and closing file descriptor 3 for reading and file descriptor 4 for writing. The main will also create 2 different fifos with code 0777 allowing permissions for both processes and it will open fifofd in reading and writing mode, and fifo2fd will open in reading and writing mode with 0777 aswell, then a signal is extablished to SIGUSR1 for each action that occurs in the program.

player 1: uses a signal and uses pause() to suspend the process until a signal is recieved this is done in a infinite wwhile loop, if the points are greater than 40 or equal to 40 then a signal will be sent using kill() getting the parent process and sending it to SIGUSR1

player 2: uses to file descriptors that act as pipes fd[1] as writing and fd[0] as readding. This is done in an infinite while loop using read() function to read the pipe into fd[0] once again if the points are greater than or equal to 40 points then the program will use kill() to send a signal to terminate the process and write it into fd[1] into a variable nme called turn.

player3: uses 2 fifo's and uses a infinite while loop to read the fifo into turn taking 1 byte at a time. if the points are greater than or equal to 40 then a signal will be sent using kill() to terminate the process. Then it will write the players turn into fifo2.

