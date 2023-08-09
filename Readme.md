# Thread

This blog may be too long, But this is everything you need to know from basic to advanced about Thread in Android.

## What is Thread in Java?

Java is a multi-threaded programming language which means we can develop multi-threaded program using Java. A multi-threaded program contains two or more parts that can run concurrently and each part can handle a different task at the same time making optimal use of the available resources specially when your computer has multiple CPUs.

By definition, multitasking is when multiple processes share common processing resources such as a CPU. Multi-threading extends the idea of multitasking into applications where you can subdivide specific operations within a single application into individual threads. Each of the threads can run in parallel. The OS divides processing time not only among different applications, but also among each thread within an application.

## Life Cycle

![alt_text](https://miro.medium.com/v2/resize:fit:786/format:webp/1*Dfl8EQlWdIebwAh9UinLMA.jpeg)

### New

Before the execution thread, a Thread object is created. At this point, the thread is not alive. It remains this state until the program starts the thread by calling Thread.start().

### Runnable

When we call Thread.start(), the thread’s state is changed to Runnable. The execution environment is set up and the thread is ready to be executed. The control is given to thread scheduler to finish its execution. Whether to run this thread instantly or keep it in runnable thread pool before running, depends on the implementation of thread scheduler.

### Running

Thread scheduler picks one of the thread from the runnable thread pool and change its state to Running. The run() method is called and the task is executed.

### Blocked

A thread can enter Blocked state due to waiting for the resources that are held by another thread.

* Waiting for I/O resources
* Waiting for a monitor lock

After the resources are ready or monitor lock is acquired, the thread’s state is changed to Runnable and it’s moved back to runnable thread pool.

### Waiting

A thread is in the waiting state due to calling one of the following methods:

* Object.wait with no timeout
* Thread.join with no timeout
  A thread in the waiting state is waiting for another thread to perform a particular action. For example, a thread that has called Object.wait() on an object is waiting for another thread to call Object.notify() or Object.notifyAll() on that object.

Once the thread wait state is over, it’s state is changed to Runnable and it’s moved back to runnable thread pool.

### Timed_Waiting

A thread is in the timed waiting state due to calling one of the following methods with a specified positive waiting time:

* Thread.sleep
* Object.wait with timeout
* Thread.join with timeout

Once the thread wait state is over, its state is changed to Runnable and it’s moved back to runnable thread pool.

### Terminated

When the run() method has finished execution, the thread is terminated and its resources can be freed up. This is the final state of the thread and no reuse of the thread instance or its execution environment is possible.

## Thread Priorities

Every Java thread has a priority that helps the operating system determine the order in which threads are scheduled.

Java thread priorities are in the range between MIN_PRIORITY (a constant of 1) and MAX_PRIORITY (a constant of 10). By default, every thread is given priority NORM_PRIORITY (a constant of 5).

Threads with higher priority are more important to a program and should be allocated processor time before lower-priority threads. However, thread priorities cannot guarantee the order in which threads execute and are very much platform dependent.

In Android, The Process class helps reduce complexity in assigning priority values by providing a set of constants that your app can use to set thread priorities. For example, THREAD_PRIORITY_DEFAULT represents the default value for a thread. Your app should set the thread's priority to THREAD_PRIORITY_BACKGROUND for threads that are executing less-urgent work.
Your app can use the THREAD_PRIORITY_LESS_FAVORABLE and THREAD_PRIORITY_MORE_FAVORABLE constants as incrementers to set relative priorities. For a list of thread priorities, see the THREAD_PRIORITY constants in the Process class.

## Creating a Thread

### Extend Syntax

```java
public class Main extends Thread {
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

### Implement Syntax

```java
public class Main implements Runnable {
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

## Running Threads

### Extend Example

```java
public class Main extends Thread {
  public static void main(String[] args) {
    Main thread = new Main();
    thread.start();
    System.out.println("This code is outside of the thread");
  }
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

### Implement Example

```java
public class Main implements Runnable {
  public static void main(String[] args) {
    Main obj = new Main();
    Thread thread = new Thread(obj);
    thread.start();
    System.out.println("This code is outside of the thread");
  }
  public void run() {
    System.out.println("This code is running in a thread");
  }
}
```

## Thread Methods

Important methods in the Thread class


| Sr.No. | Method & Description                                                                                                                                                                                                             |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | **public void start()**<br />Starts the thread in a separate path of execution, then invokes the run() method on this Thread object.                                                                                             |
| 2      | **public void run()**<br />If this Thread object was instantiated using a separate Runnable target, the run() method is invoked on that Runnable object.                                                                         |
| 3      | **public final void setName(String name)**<br />Changes the name of the Thread object. There is also a getName() method for retrieving the name.                                                                                 |
| 4      | **public final void setPriority(int priority)**<br />Sets the priority of this Thread object. The possible values are between 1 and 10.                                                                                          |
| 5      | **public final void setDaemon(boolean on)**<br />A parameter of true denotes this Thread as a daemon thread.                                                                                                                     |
| 6      | **public final void join(long millisec)**<br />The current thread invokes this method on a second thread, causing the current thread to block until the second thread terminates or the specified number of milliseconds passes. |
| 7      | **public void interrupt()**<br />Interrupts this thread, causing it to continue execution if it was blocked for any reason.                                                                                                      |
| 8      | **public final boolean isAlive()**<br />Returns true if the thread is alive, which is any time after the thread has been started but before it runs to completion.                                                               |

The previous methods are invoked on a particular Thread object. The following methods in the Thread class are static. Invoking one of the static methods performs the operation on the currently running thread.


| Sr.No. | Method & Description                                                                                                                                         |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | **public static void yield()**<br />Causes the currently running thread to yield to any other threads of the same priority that are waiting to be scheduled. |
| 2      | **public static void sleep(long millisec)**<br />Causes the currently running thread to block for at least the specified number of milliseconds.             |
| 3      | **public static boolean holdsLock(Object x)**<br />Returns true if the current thread holds the lock on the given Object.                                    |
| 4      | **public static Thread currentThread()**<br />Returns a reference to the currently running thread, which is the thread that invokes this method.             |
| 5      | **public static void dumpStack()**<br />Prints the stack trace for the currently running thread, which is useful when debugging a multithreaded application. |

## =================== Let's take a break =====================

We already know what is Thread and how to run it. But while doing Multi threading programming we need to know following concepts very handy

## Major Java Multithreading Concepts

When we start two or more threads within a program, there may be a situation when multiple threads try to access the same resource and finally they can produce unforeseen result due to concurrency issues. For example, if multiple threads try to write within a same file then they may corrupt the data because one of the threads can override data or while one thread is opening the same file at the same time another thread might be closing the same file.

So there is a need to synchronize the action of multiple threads and make sure that only one thread can access the resource at a given point in time. This is implemented using a concept called monitors. Each object in Java is associated with a monitor, which a thread can lock or unlock. Only one thread at a time may hold a lock on a monitor.

Java programming language provides a very handy way of creating threads and synchronizing their task by using synchronized blocks.

For Example:

```java
synchronized(objectidentifier) {
   // Access shared variables and other shared resources
}
```

Here, the objectidentifier is a reference to an object whose lock associates with the monitor that the synchronized statement represents.

Now let's practice with bellow example.

### Multithreading Example without Synchronization

#### Example

```java
class PrintDemo {
   public void printCount() {
      try {
         for(int i = 5; i > 0; i--) {
            System.out.println("Counter   ---   "  + i );
         }
      } catch (Exception e) {
         System.out.println("Thread  interrupted.");
      }
   }
}

class ThreadDemo extends Thread {
   private Thread t;
   private String threadName;
   PrintDemo  PD;

   ThreadDemo( String name,  PrintDemo pd) {
      threadName = name;
      PD = pd;
   }
   
   public void run() {
      PD.printCount();
      System.out.println("End " +  threadName + " exiting.");
   }

   public void start () {
      System.out.println("Starting " +  threadName );
      if (t == null) {
         t = new Thread (this, threadName);
         t.start ();
      }
   }
}

public class TestThread {
   public static void main(String args[]) {

      PrintDemo PD = new PrintDemo();

      ThreadDemo T1 = new ThreadDemo( "Thread - 1 ", PD );
      ThreadDemo T2 = new ThreadDemo( "Thread - 2 ", PD );

      T1.start();
      T2.start();

      // wait for threads to end
         try {
         T1.join();
         T2.join();
      } catch ( Exception e) {
         System.out.println("Interrupted");
      }
   }
}
```

Output:

```json
Starting Thread - 1
Starting Thread - 2
Counter   ---   5
Counter   ---   4
Counter   ---   3
Counter   ---   5
Counter   ---   2
Counter   ---   1
Counter   ---   4
End Thread - 1  exiting.
Counter   ---   3
Counter   ---   2
Counter   ---   1
End Thread - 2  exiting.
```

### Multithreading Example with Synchronization

Now, Change above example with Synchronization solution:

```java
class PrintDemo {
   public void printCount() {
      try {
         for(int i = 5; i > 0; i--) {
            System.out.println("Counter   ---   "  + i );
         }
      } catch (Exception e) {
         System.out.println("Thread  interrupted.");
      }
   }
}

class ThreadDemo extends Thread {
   private Thread t;
   private String threadName;
   PrintDemo  PD;

   ThreadDemo( String name,  PrintDemo pd) {
      threadName = name;
      PD = pd;
   }
   
   public void run() {
      synchronized(PD) {
         PD.printCount();
      }
      System.out.println("End " +  threadName + " exiting.");
   }

   public void start () {
      System.out.println("Starting " +  threadName );
      if (t == null) {
         t = new Thread (this, threadName);
         t.start ();
      }
   }
}

public class TestThread {

   public static void main(String args[]) {
      PrintDemo PD = new PrintDemo();

      ThreadDemo T1 = new ThreadDemo( "Thread - 1 ", PD );
      ThreadDemo T2 = new ThreadDemo( "Thread - 2 ", PD );

      T1.start();
      T2.start();

      // wait for threads to end
      try {
         T1.join();
         T2.join();
      } catch ( Exception e) {
         System.out.println("Interrupted");
      }
   }
}
```

Output

```json
Starting Thread - 1
Starting Thread - 2
Counter   ---   5
Counter   ---   4
Counter   ---   3
Counter   ---   2
Counter   ---   1
End Thread - 1  exiting.
Counter   ---   5
Counter   ---   4
Counter   ---   3
Counter   ---   2
Counter   ---   1
End Thread - 2  exiting.
```

## Interthread Communication

If you are aware of interprocess communication then it will be easy for you to understand interthread communication. Interthread communication is important when you develop an application where two or more threads exchange some information.
There are three simple methods and a little trick which makes thread communication possible.


| Sr.No. | Method & Description                                                                                     |
| -------- | ---------------------------------------------------------------------------------------------------------- |
| 1      | **public void wait()**<br />Causes the current thread to wait until another thread invokes the notify(). |
| 2      | **public void notify()**<br />Wakes up a single thread that is waiting on this object's monitor.         |
| 3      | **public void notifyAll()**<br />Wakes up all the threads that called wait( ) on the same object.        |

These methods have been implemented as final methods in Object, so they are available in all the classes. All three methods can be called only from within a synchronized context.

```java
class Chat {
   boolean flag = false;

   public synchronized void Question(String msg) {
      if (flag) {
         try {
            wait();
         } catch (InterruptedException e) {
            e.printStackTrace();
         }
      }
      System.out.println(msg);
      flag = true;
      notify();
   }

   public synchronized void Answer(String msg) {
      if (!flag) {
         try {
            wait();
         } catch (InterruptedException e) {
            e.printStackTrace();
         }
      }

      System.out.println(msg);
      flag = false;
      notify();
   }
}

class T1 implements Runnable {
   Chat m;
   String[] s1 = { "Hi", "How are you ?", "I am also doing fine!" };

   public T1(Chat m1) {
      this.m = m1;
      new Thread(this, "Question").start();
   }

   public void run() {
      for (int i = 0; i < s1.length; i++) {
         m.Question(s1[i]);
      }
   }
}

class T2 implements Runnable {
   Chat m;
   String[] s2 = { "Hi", "I am good, what about you?", "Great!" };

   public T2(Chat m2) {
      this.m = m2;
      new Thread(this, "Answer").start();
   }

   public void run() {
      for (int i = 0; i < s2.length; i++) {
         m.Answer(s2[i]);
      }
   }
}
public class TestThread {
   public static void main(String[] args) {
      Chat m = new Chat();
      new T1(m);
      new T2(m);
   }
}
```

### Result:

```json
Hi
Hi
How are you ?
I am good, what about you?
I am also doing fine!
Great!
```

## Thread Deadlock

Deadlock describes a situation where two or more threads are blocked forever, waiting for each other. Deadlock occurs when multiple threads need the same locks but obtain them in different order. A Java multithreaded program may suffer from the deadlock condition because the synchronized keyword causes the executing thread to block while waiting for the lock, or monitor, associated with the specified object

### Example:

```java
public class TestThread {
   public static Object Lock1 = new Object();
   public static Object Lock2 = new Object();
   
   public static void main(String args[]) {
      ThreadDemo1 T1 = new ThreadDemo1();
      ThreadDemo2 T2 = new ThreadDemo2();
      T1.start();
      T2.start();
   }
   
   private static class ThreadDemo1 extends Thread {
      public void run() {
         synchronized (Lock1) {
            System.out.println("Thread 1: Holding lock 1...");
          
            try { Thread.sleep(10); }
            catch (InterruptedException e) {}
            System.out.println("Thread 1: Waiting for lock 2...");
          
            synchronized (Lock2) {
               System.out.println("Thread 1: Holding lock 1 & 2...");
            }
         }
      }
   }
   private static class ThreadDemo2 extends Thread {
      public void run() {
         synchronized (Lock2) {
            System.out.println("Thread 2: Holding lock 2...");
          
            try { Thread.sleep(10); }
            catch (InterruptedException e) {}
            System.out.println("Thread 2: Waiting for lock 1...");
          
            synchronized (Lock1) {
               System.out.println("Thread 2: Holding lock 1 & 2...");
            }
         }
      }
   } 
}
```

### Output

```json
Thread 1: Holding lock 1...
Thread 2: Holding lock 2...
Thread 1: Waiting for lock 2...
Thread 2: Waiting for lock 1...
```

### Solution Example

```java
public class TestThread {
   public static Object Lock1 = new Object();
   public static Object Lock2 = new Object();
   
   public static void main(String args[]) {
      ThreadDemo1 T1 = new ThreadDemo1();
      ThreadDemo2 T2 = new ThreadDemo2();
      T1.start();
      T2.start();
   }
   
   private static class ThreadDemo1 extends Thread {
      public void run() {
         synchronized (Lock1) {
            System.out.println("Thread 1: Holding lock 1...");
          
            try {
               Thread.sleep(10);
            } catch (InterruptedException e) {}
            System.out.println("Thread 1: Waiting for lock 2...");
          
            synchronized (Lock2) {
               System.out.println("Thread 1: Holding lock 1 & 2...");
            }
         }
      }
   }
   private static class ThreadDemo2 extends Thread {
      public void run() {
         synchronized (Lock1) {
            System.out.println("Thread 2: Holding lock 1...");
         
            try {
               Thread.sleep(10);
            } catch (InterruptedException e) {}
            System.out.println("Thread 2: Waiting for lock 2...");
          
            synchronized (Lock2) {
               System.out.println("Thread 2: Holding lock 1 & 2...");
            }
         }
      }
   } 
}
```

### Output

```json
Thread 1: Holding lock 1...
Thread 1: Waiting for lock 2...
Thread 1: Holding lock 1 & 2...
Thread 2: Holding lock 1...
Thread 2: Waiting for lock 2...
Thread 2: Holding lock 1 & 2...
```

## Thread Control

Core Java provides complete control over multithreaded program. You can develop a multithreaded program which can be suspended, resumed, or stopped completely based on your requirements.


| Sr.No. | Method & Description                                                                                                      |
| -------- | --------------------------------------------------------------------------------------------------------------------------- |
| 1      | **public void suspend()**<br />This method puts a thread in the suspended state and can be resumed using resume() method. |
| 2      | **public void stop()**<br />This method stops a thread completely.                                                        |
| 3      | **public void resume()**<br />This method resumes a thread, which was suspended using suspend() method.                   |
| 4      | **public void wait()**<br />Causes the current thread to wait until another thread invokes the notify().                  |
| 5      | **public void notify()**<br />Wakes up a single thread that is waiting on this object's monitor.                          |



## ======================== It's too long and boring...I tried to much to continue writing :( =======================
