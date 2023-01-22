# Quable Apex

- enables you to add jobs to the queue and monitor them. This enhanced way of running your asynchronous Apex code compared to using future methods.
- Additional benefitis compaired to future method:

1. Getting an ID for your job
2. Using non-primitive types - using constructor
3. Chaining jobs

``` java
public class AsyncExecutionExample implements Queueable {
    public void execute(QueueableContext context) {
        Account a = new Account(Name='Acme',Phone='(415) 555-1212');
        insert a;        
    }
}
```

``` java
ID jobID = System.enqueueJob(new AsyncExecutionExample());

```

## Delay to Queueable Jobs


``` java
Integer delayInMinutes = 5;
ID jobID = System.enqueueJob(new AsyncExecutionExample(), delayInMinutes);
```

>**Org Wide Delay**
>
>From Setup, in the Quick Find box, enter Apex Settings, and then enter a value (1–600 seconds) for Default minimum enqueue delay (in seconds) for queueable jobs that do not have a delay parameter
