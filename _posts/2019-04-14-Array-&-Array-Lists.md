---
layout: post
title: "Array & Array Lists"
date: 2019-04-14 11:46:10 +03:00
description: "This is meta description"
featured: true
image: "assets/images/featured-post/arrayandarraylist.jpg"
categories: 
  - "Kaiden"
---
<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/7de4ba0b-2fac-4945-8a15-cc3570b0c519" alt="Image 1">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/4a9f058f-3242-48e0-9da5-ba2026ccdac9" alt="Image 2">
</div>

## What is happening?
This code is for a high school clube that desires to store their club members with their name, the graduation year, and if they are in good standing.

```Java
import java.util.ArrayList;
public class MemberInfo{ // filling in the code that College Board did not provide
    private String name;
    private int gradYear;
    private boolean hasGoodStanding;
    public MemberInfo(String name, int gradYear, boolean hasGoodStanding){
        this.name = name;
        this.gradYear = gradYear;
        this.hasGoodStanding = hasGoodStanding;
    }
    public int getGradYear(){
        return gradYear;
    }
    public boolean inGoodStanding(){
        return hasGoodStanding;
    }
    
    public String getName() {
        return name;
    }
}
```

<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/06179dcd-e6fb-4d66-b88e-ca64ce4ee712" alt="Image 3">
</div>

## Part A
This question wants me to create a method that allows the club to add members to the the MemberInfo ArrayList. They want to be able to add a bunch of names under the same graduation year.

```Java
public class ClubMembers{
    private ArrayList<MemberInfo> memberList;
    public ArrayList<MemberInfo> getMemberList() {
        return memberList;
    }
    public ClubMembers(){
        memberList = new ArrayList<>(); // making the empty memberList
    }
    public void addMember (String[] names, int gradYear){
        for (int i = 0; i < names.length; i++){
            MemberInfo mem = new MemberInfo(names[i], gradYear, true); // iterating through each person and adding them as good standing
            memberList.add(mem);
        }
    }
    public ArrayList<MemberInfo> removeMembers(int year){
        ArrayList<MemberInfo> remove = new ArrayList<>();
        for (int i = memberList.size()-1; i>=0;i--){ // iterating through everyone and seeing if they are too low of year, and then deleting them. If they are not in good standing they are not returned, but are returned if are in good standing
            MemberInfo member = memberList.get(i);
            if (member.getGradYear() <= year){
                if(member.inGoodStanding()){
                    remove.add(member);
                }
                memberList.remove(i);
            }
        }
        return remove;
    }
}
```
```Java
public class ClubMembersTest {
    public static void main(String[] args) {
        ClubMembers myclub = new ClubMembers();
        String[] names = {"Tim", "Jim", "Bim"};
        myclub.addMember(names, 1999);
        System.out.println("inital adders");
        for (MemberInfo member : myclub.getMemberList()) {
            System.out.println(member.getName() + " - Grad Year: " + member.getGradYear());
        }
        String[] newnames = {"Joe","Toe"};
        myclub.addMember(newnames, 2000);
        System.out.println("new adders");
        for (MemberInfo member : myclub.getMemberList()) {
            System.out.println(member.getName() + " - Grad Year: " + member.getGradYear());
        }
        ArrayList<MemberInfo> removeMembers = myclub.removeMembers(1999);
        System.out.println("remove 1999");
        for (MemberInfo member : removeMembers) {
            System.out.println(member.getName() + " - Grad Year: " + member.getGradYear());
        }
        System.out.println("remaining");
        for (MemberInfo member : myclub.getMemberList()) {
            System.out.println(member.getName() + " - Grad Year: " + member.getGradYear());
        }
    }
}
ClubMembersTest.main(null);
```

    inital adders
    Tim - Grad Year: 1999
    Jim - Grad Year: 1999
    Bim - Grad Year: 1999
    new adders
    Tim - Grad Year: 1999
    Jim - Grad Year: 1999
    Bim - Grad Year: 1999
    Joe - Grad Year: 2000
    Toe - Grad Year: 2000
    remove 1999
    Bim - Grad Year: 1999
    Jim - Grad Year: 1999
    Tim - Grad Year: 1999
    remaining
    Joe - Grad Year: 2000
    Toe - Grad Year: 2000

### Part A Explanation
In this code block, I had it iterate through each name and add the name and graduation year that is provided and add the default good standing to each person and add it to the memberlist.


<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/2c9ca642-b1ed-412f-89ce-0318222c3e13" alt="Image 4">
</div>

## Part B
This question wants me to be able to remove members by their graduation year. It wants to record the removed members only if they have good standing.

### Part B Explanation
This one, I had to record the members that had good standing but were getting removed. Also I would remove the members with grad year that is the provided year or lower. Only the good standing are recorded, otherwise it is only deleted.

## Grading

| Requirement | Points Gained | Reasoning |
|:---:|---|:---:|
|A|||
| Accesses all elements of names (no bounds errors) | 1/1 | line 8: MemberInfo mem = new MemberInfo(names[i], gradYear, true);|
| Instantiates a MemberInfo object with name from array, provided year, and good standing | 1/1 | MemberInfo mem = new MemberInfo(names[i], gradYear, true); |
| Adds MemberInfo objects to memberList (in the context of a loop) | 1/1 | MemberList.add(mem); |
|B|||
| Declares and initializes an ArrayList of MemberInfo objects | 1/1 |ArrayList<MemberInfo> remove = new ArrayList<>();|
| Accesses all elements of memberList for potential removal (no bounds errors) | 1/1 |for (int i = memberList.size()-1; i>=0;i--){<br>MemberInfo member = memberList.get(i);|
| Calls getGradYear or inGoodStanding | 1/1 |if (member.getGradYear() <= year){<br>if(member.inGoodStanding()){|
| Distinguishes any three cases based on graduation status and standing | 1/1 |Yes|
| Indentifies graduating members | 1/1 |Yes|
| Removes appropriate members from memberList and adds appropriate members to the ArrayList to be returned | 1/1 |remove.add(member);|


<style>
  .images {
    border: 1px solid black;
  }
</style>