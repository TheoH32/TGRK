---
layout: post
title: "Array & Array Lists"
date: 2019-04-14 11:46:10 +03:00
description: "This is meta description"
featured: true
image: "assets/images/featured-post/arrayandarraylist.jpg"
categories: 
  - "Kaiden"
  - "FRQs"
---
<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/7de4ba0b-2fac-4945-8a15-cc3570b0c519" alt="Image 1">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/4a9f058f-3242-48e0-9da5-ba2026ccdac9" alt="Image 2">
</div>

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
}
```

<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/06179dcd-e6fb-4d66-b88e-ca64ce4ee712" alt="Image 3">
</div>

```Java
public class ClubMembers{
    private ArrayList<MemberInfo> memberList;
    public ClubMembers(){
        memberList = new ArrayList<>(); // making the empty memberList
    }
    public void addMember (String[] names, int gradYear){
        for (int i = 0; i < names.length; i++){
            MemberInfo mem = new MemberInfo(names[i], gradYear, true); // iterating through each person and adding them as good standing
            MemberList.add(mem);
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

In this code block, I had it iterate through each name and add the name and graduation year that is provided and add the default good standing to each person and add it to the memberlist.


<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/2c9ca642-b1ed-412f-89ce-0318222c3e13" alt="Image 4">
</div>

This one, I had to record the members that had good standing but were getting removed. Also I would remove the members with grad year that is the provided year or lower. Only the good standing are recorded, otherwise it is only deleted.


<style>
  .images {
    border: 1px solid black;
  }
</style>