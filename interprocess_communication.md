### *Hain Lukas*
# Processes Communication
## 1. Race Condition
When multiple processes share the same variables and one process overwrites the values of the other ones with his own.

## 2. Disabling Interrupts
  1. Because desabling interrupts only effects the core the interrupts were disabled on.
  2. Because if the process for example enters an infinite loop, every other process has to wait for the infinite loop to end, wich it never will, and the mashine will just stop working.

## 3. Peterson´s Solution

  1.

    1. Process 0 sets itself to interested and to the one who has to wait, but since no other process is interested, process 0 enters the CR.
    Process 1 sets itself to interested and to the one who has to wait, but process 0 is still set to interested, so process 1 has to wait.
    Process 0 leaves the CR and sets itself to not interested.
    Process 1 sees that no other process is interested, so it enters the CR.

    2. Process 0 is slightly faster than process 1, so process 1 sets itself to the one who has to wait, while process 0 enters the CR.
    Process 0 leaves the CR and sets itself to not interested.
    Process 1 sees that no other process is interested, so it enters the CR.

  2.

    Process 0 has higher priority than process 1 -> process 0 moves 8 times, process 1 moves once.
    Process 0 goes enters the CR, leaves the CR and sets turn to 1.
    process 1 verifies, that it can enter the CR.
    Process 0 now tries to enter the CR over and over again, but cannot, because process 1 has not set turn to 0 yet.

  3.

    The loser in Peterson´s solution is the process, that has to wait for the other one to leave the CR, only then can it enter the CR itself.
    When both processes are set to interested, the loser has to wait for the other process to finish the CR.

  4.


    int loser;

    Bool interested[3];

    int process_count = 3;


    void enter_region(int process)

    {

      interested[process] = True;

      loser = process;

      bool others_are_interested = false;

      for(int i = 0; i < process_count; i++) {

        if(interested[i] && i != process) {

          others_are_interested = true;

        }

      }

      while (loser == process && others_are_interested) ;

    }



    void leave_region(int process)

    {

      interested[process] = False;

    }
