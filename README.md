
# Starve_free_readers_writers_problem
int readcount; ( 
// Number of readers accessing resources
// initial value = 0 )
## semaphores used
```
semaphore mutex, read, write; 
// initial values of all semaphores = 1
```
```
  wait(semaphore){
    if(semaphore <= 0){
    // do nothing
    }
    else{
    semaphore--;
    }
  signal(semaphore){
      semaphore++
    }
 ```
    
## //READERS CODE
    reader(){
    wait(read);
      wait(mutex);
        readcount++;
        if (readcount == 1)
          wait(write);
      signal(mutex);          
    signal(read);

    // reading is performed 

    wait(mutex);
      readcount--;
      if(readcount == 0)
        signal(write);
    signal(mutex);
    }
    
## //WRITERS CODE
```
  writer(){
    wait(read);
    wait(write);

     // writing is performed

    signal(write);  
    signal(read);
    }
 ```
    
  ## Solution 
  read,write semaphores ensures that only one of them can access resource and mutex ensures readcount value change correctly.
  Here any number of of readers can read at a time and only one writer can write at a time.It is given turns so there will be no starvation for either readers or writers.
 ### References
 - Operating System Concepts by Abraham Silberschatz, Peter B. Galvin, Greg Gagne -PSK sir's Slides
 + Wikipedia
