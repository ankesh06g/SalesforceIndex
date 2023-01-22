# Schedule Apex

- To schedule an Apex class to run on a specific schedule
- We can only have 100 scheduled Apex jobs at one time
- We can call any Sync or Async apex

## Cron Expression

| Name | Values | Special Chars |
|-------|--------|----------|
|Seconds|0-59||
|Minuts|0-59||
|Hours|0-23||
|Day of month | 1-31|,-*?/LW|
|Month|1-12, JAN-DEC|,-*/|
|Day of week|1-7, SUN-SAT|,-*?/L#|
|Optional Year|null, 1970-2099|,-*/|

> , : Multiple Values
> - : Range
> * : All Possible Values
> ? : Do not Specify any value
> / : Specifies increment
> L : Last possible value
> W : Closest week day

``` java
global class ScheduledMerge implements Schedulable {
   global void execute(SchedulableContext SC) {
      // Any apex code
   }
}
```

``` java
ScheduledMerge m = new ScheduledMerge();
String sch = '20 30 8 10 2 ?';
String jobID = System.schedule('Merge Job', sch, m);
```

> **NOTE:**
>
> To stop any schedule job we can use ```System.abortJob(JobId)```

## Tracking the Progress

``` java
CronTrigger ct = 
    [SELECT TimesTriggered, NextFireTime
    FROM CronTrigger WHERE Id = :jobID];
```

If we were performing this query inside the execute method of schedulable class

``` java
CronTrigger ct = 
    [SELECT TimesTriggered, NextFireTime
    FROM CronTrigger WHERE Id = :sc.getTriggerId()];
```

