---
author: varokas
comments: true
date: 2014-06-28 22:43:23+00:00
layout: post
slug: async-testing-%e0%b8%9a%e0%b8%99-javascript
title: Async Testing บน JavaScript
wordpress_id: 640
categories:
- Software Engineering
tags:
- js
- testing
---

ใช้ Asynchronous โค้ดมักจะเทสได้ยาก เพราะเราไม่รู้ว่ามันจะไปจบลงเมื่อไหร่ เพราะเวลาเราเรียกฟังก์ชัน async เสร็จมันก็จะไปอยู่ในโลกของมันเอง ไม่กลับมาอีก

<!--more-->ซึ่งเทคนิคในการแก้ไขแบบนี้น่าจะมีได้หลายแบบ อย่างนึงที่คิดออกและเคยทำคือ ต้องให้ async code มันไปเขียนค่าใน shared variable ซักตัวนึง แล้วก็ให้เทสมันเช็คหลังจากรอไปซักพักนึง

แต่สำหรับ JavaScript ถ้าใครใช้ jasmine เป็นเฟรมเวิร์คในการเทส จะมีวิธีจัดการง่ายๆ แบบนี้

[code lang="js"]
it("async spec must use done callback", function(done) {
  setTimeout(function() {
    done();
  }
  ,50);
});
[/code]

ลองสังเกตว่าถ้าเราเขียนเทสปกติ function ที่อยู่ใน it(..) จะไม่รับ parameter อะไร แต่ถ้าเป็นแบบ async ก็จะมีการประกาศตัวแปรขึ้นมา 1 ตัว (ไม่ให้งงแนะนำว่าให้ใช้ชื่อว่า done) ซึ่งถ้าประกาศแบบนี้แล้ว jasmine ก็จะรู้เองว่าเราอยากใช้แบบ async ซึ่งจะผ่านเมื่อในโค้ดเรามีการเรียก done ก่อนเวลา timeout (ค่า default คือ 5 วินาที เปลี่ยนได้)

ลองไปรันโค้ดได้จากที่นี่ : [[https://github.com/varokas/kata-js](https://github.com/varokas/kata-js)]
