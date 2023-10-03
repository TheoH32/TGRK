---
layout: post
title: Methods and Control Structures
date: 2019-04-14 14:46:12 +03:00
description: "This is the fist collegeboard FRQ in our presentation"
featured: true
image: "assets/images/featured-post/methods.jpg"
categories: 
  - "Grace"
---

## FRQ #1 - Methods and Control Structures
This question involves the AppointmentBook class, which provides methods for students to schedule appointments with their teacher. Appointments can be scheduled during one of eight class periods during the school day, numbered 1 through 8. A requested appointment has a duration, which is the number of mins the appointment will last. The 60 minutes within a period are numbered 0 through 59. In order for an appointment to be scheduled, the teacher must have a block of consecutive, available minutes that contains at least the requested number of minutes in a requested period. Scheduled appointments must start and end within the same period.

![Question](https://media.discordapp.net/attachments/1010780182476496908/1151949183197139034/image.png?width=842&height=998)

## Part A

![Part a](https://media.discordapp.net/attachments/1010780182476496908/1151949486470484119/image.png?width=912&height=998)


```Java
public int findFreeBlock(int period, int duration)
{
    int free = 0;
    
    for(int min = 0; min <= 59; min++)
    {
        if(isMinuteFree(period, minute))
            free++;
        else
            free = 0;
        
        if(free == duration)
            return min - free + 1;
    }
    
    return -1;
}
```

## Part B

![Part B_1](https://media.discordapp.net/attachments/1010780182476496908/1151956661628575804/image.png?width=826&height=998)

![Part B_2](https://media.discordapp.net/attachments/1010780182476496908/1151956694650322955/image.png?width=1256&height=998)


```Java
public boolean makeAppointment(int start, int end, int duration)
{
    for(int period = start; period <= end; period++)
    {
        int startMinute = findFreeBlock(period, duration);
        if(startMinute != -1)
        {
            reserveBlock(period, startMinute, duration);
            return true;
        }
    }
    return false;
}
```

## Part 3
Array Experimentation


```Java
String Foods;
String[] Foods = {"Burrito", "Pasta", "Tacos", "Rice"};
System.out.println(Foods[0])
```

    Burrito



```Java
System.out.println(Foods.length);
```

    4


Now we will go with 2D Arrays, this is some experimentation


```Java
int[][] arr = { { 1, 2 }, { 3, 4 } };
System.out.println("Pos 0: " + arr[0][0] + ", " + arr[0][1]);
System.out.println("Pos 1: " + arr[1][0] + ", " + arr[1][1]);
```

    Pos 0: 1, 2
    Pos 1: 3, 4


## Part 4 -- Array Implimentation
### Part A
There is only one variable here so it would not really make sense to put an array for a static variable that we are only changing to determine the time; ie we need no history of the variable as well.


```Java
public int findFreeBlock(int period, int duration)
{
    int free = 0;
    
    for(int min = 0; min <= 59; min++)
    {
        if(isMinuteFree(period, minute))
            free++;
        else
            free = 0;
        
        if(free == duration)
            return min - free + 1;
    }
    
    return -1;
}
```

### Part B
Since we only use one variable here, pulling only one definate value from a function, it would be impractical to use an array here. 


```Java
public boolean makeAppointment(int start, int end, int duration)
{
    for(int period = start; period <= end; period++)
    {
        int startMinute = findFreeBlock(period, duration);
        if(startMinute != -1)
        {
            reserveBlock(period, startMinute, duration);
            return true;
        }
    }
    return false;
}
```

### Part A -- Implimented


```Java
public int findFreeBlock(int period, int duration)
{
    int[] free = {0};
    
    for(int min = 0; min <= 59; min++)
    {
        if(isMinuteFree(period, minute))
            free[0]++;
        else
            free[0] = 0;
        
        if(free[0] == duration)
            return min - free + 1;
    }
    
    return -1;
}
```

## Part 5: Project with Arrays with Methods and Control Structures


```Java
public int transform(int original)
{
    int[] transformers = {1, -1, 2, -3, 5, -8, 13, -21};

    for(int i = 0; i <= 7; i++)
    {
        // original = original + transformers[i];
        if(original < 0)
            original = (transformers[i] * original) - transformers[i];
        else
            original = (transformers[i] * original) + transformers[i];
    }
    return original;
}
```


```Java
transform(100)
```




    6794718




```Java
transform(-1)
```




    -308238




```Java
transform(0.5)
```


    |   transform(0.5)

    incompatible types: possible lossy conversion from double to int

    



```Java
transform(-300)
```




    -19898718




```Java
transform(0)
```




    242718



## Complete Code Execution


```Java
public class AppointmentBook
{
    // package access for testing
    // [period - 1][minute]
    boolean[][] freeMinutes;
    
    public AppointmentBook()
    {
        freeMinutes = new boolean[8][60];
        
        for(int r = 0; r < freeMinutes.length; r++)
            for(int c = 0; c < freeMinutes[0].length; c++)
                freeMinutes[r][c] = true;
    }
    
    private boolean isMinuteFree(int period, int minute)
    {
        return freeMinutes[period - 1][minute];
    }
    
    // package access for testing
    void reserveBlock(int period, int startMinute, int duration)
    {
        for(int minute = startMinute; minute < startMinute + duration; minute++)
            freeMinutes[period - 1][minute] = false;
    }
    
    public int findFreeBlock(int period, int duration)
    {
        int freeInARow = 0;
        
        for(int minute = 0; minute <= 59; minute++)
        {
            if(isMinuteFree(period, minute))
                freeInARow++;
            else
                freeInARow = 0;
            
            if(freeInARow == duration)
                return minute - freeInARow + 1;
        }
        
        return -1;
    }
    
    public boolean makeAppointment(int startPeriod, int endPeriod,
                                   int duration)
    {
        for(int period = startPeriod; period <= endPeriod; period++)
        {
            int startMinute = findFreeBlock(period, duration);
            
            if(startMinute != -1)
            {
                reserveBlock(period, startMinute, duration);
                return true;
            }
        }
        
        return false;
    }
}
```


```Java
import java.util.Arrays;
//import org.junit.Test;
//import org.junit.Assert;

public class OneTest
{
    public void testFindFreeBlockAgainstExamples()
    {
        AppointmentBook book = new AppointmentBook();
        
        book.reserveBlock(2, 0, 10);
        book.reserveBlock(2, 15, 15);
        book.reserveBlock(2, 45, 5);
        
        Assert.assertTrue(book.findFreeBlock(2, 15) == 30);
        Assert.assertTrue(book.findFreeBlock(2, 9) == 30);
        Assert.assertTrue(book.findFreeBlock(2, 20) == -1);
    }
    
    public void testMakeAppointmentAgainstExamples()
    {
        AppointmentBook book = new AppointmentBook();
        
        book.reserveBlock(2, 0, 25);
        book.reserveBlock(2, 30, 30);
        book.reserveBlock(3, 15, 26);
        book.reserveBlock(4, 0, 5);
        book.reserveBlock(4, 30, 14);
        
        AppointmentBook expectedBook = new AppointmentBook();
        
        expectedBook.reserveBlock(2, 0, 25);
        expectedBook.reserveBlock(2, 30, 30);
        expectedBook.reserveBlock(3, 15, 26);
        expectedBook.reserveBlock(4, 0, 5);
        expectedBook.reserveBlock(4, 30, 14);
        
        expectedBook.reserveBlock(4, 5, 22);
        
        Assert.assertTrue(book.makeAppointment(2, 4, 22));
        Assert.assertTrue(Arrays.deepEquals(expectedBook.freeMinutes, book.freeMinutes));
        
        expectedBook.reserveBlock(3, 0, 3);
        
        Assert.assertTrue(book.makeAppointment(3, 4, 3));
        Assert.assertTrue(Arrays.deepEquals(expectedBook.freeMinutes, book.freeMinutes));
        
        Assert.assertTrue(!book.makeAppointment(2, 4, 30));
        Assert.assertTrue(Arrays.deepEquals(expectedBook.freeMinutes, book.freeMinutes));
    }
}

```

```Java
OneTest test = new OneTest();
test.testFindFreeBlockAgainstExamples();
test.testMakeAppointmentAgainstExamples();
```

    true
    true
    true
    true
    true
    true
    true
    true
    true


### Diagram Map and Scoring
![Diagram](https://media.discordapp.net/attachments/1010780182476496908/1154474547261747220/frq1.png?width=1330&height=998)
![Scoring](https://media.discordapp.net/attachments/1010780182476496908/1154474566949806090/image.png?width=1122&height=998)
Final Score: 10/10 (All Correct) - [Vivian](https://github.com/vivianknee/FastPages/issues/50)