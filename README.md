# Starve_free_readers_writers_problem
int readcount; 
// Number of readers accessing resources
// initial value = 0

semaphore mutex, read, write; 
// initial values of all semaphores = 1  

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
    
//READERS CODE
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
    
//WRITERS CODE
  writer(){
    wait(read);
    wait(write);

     // writing is performed

    signal(write);  
    signal(read);
    }
