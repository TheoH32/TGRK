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
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/06179dcd-e6fb-4d66-b88e-ca64ce4ee712" alt="Image 3">
</div>


```java
public void addMember (String[] names, int gradYear){
    for (i = 0; i < names.size(); i++){
        MemberInfo mem = new MemberInfo(names[i], gradYear, true);
        MemberList.add(mem);
    }
}
```

In this code block, I had it iterate through each name and add the name and graduation year that is provided and add the default good standing to each person and add it to the memberlist.


<div class="images">
  <img src="https://github.com/kaiden-dough/kaidencsablog/assets/69410126/2c9ca642-b1ed-412f-89ce-0318222c3e13" alt="Image 4">
</div>

```java
public ArrayList<MemberInfo> removeMembers(int year){
    ArrayList<MemberInfo> remove = new ArrayList<MemberInfo>();
    for (i = memberList.size-1; i>=0,i--){
        if (memberList.get(i).getGradYear() <= year){
            if(memberList.get(i).inGoodStanding()){
                remove.add(memberList.get(i));
            }
            memberList.remove(i);
        }
    }
    return remove;
}
```

This one, I had to record the members that had good standing but were getting removed. Also I would remove the members with grad year that is the provided year or lower. Only the good standing are recorded, otherwise it is only deleted.


<style>
  .images {
    border: 1px solid black;
  }
</style>