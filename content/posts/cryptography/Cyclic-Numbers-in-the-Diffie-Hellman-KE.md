---
title: "Cyclic Numbers in the Diffie-Hellman KE"
date: 2021-09-01T11:40:37-04:00
draft: true
tags:
    - Mathematics
    - Key Exchange
categories:
    - Cryptography
banner: images/posts/Cyclic-Numbers-in-the-Diffie-Hellman-KE/locks.jpg
---

# What is a Cyclic Number?

A cyclic number is a number where the digits are cycled when multiplied by any number. For example:
$$142857\times3=428571$$

Looking at the number, you can see that the digits have been cycled. The difference between the cyclic number and the outcome in this case is that the first digit is at the end.

All the multiples of cyclic numbers are cycles of the cyclic number.

$$142857\times1=142857$$
$$142857\times2=285714$$
$$142857\times3=428571$$
$$142857\times4=571428$$
$$142857\times5=714285$$
$$142857\times6=857142$$

See how the digits are the same as 142857, but cycled to different locations?

Let's multiple the cyclic number with a large number:

$$142857\times857=122428449$$

In this case, we can spilt the number and add both parts like the following:

$$122+428449=428571$$

We've got the same number as 

$$142857\times3=428571$$

There's more to cyclic numbers than this, but for the Diffie-Hellman Key Exchange, this understanding is sufficient. If you want to know more about it, check out the reference links.

# Why is it important in the Diffie-Hellman Key Exchange

Cyclic Numbers are important int he Diffie-Hellman Key Exchange because 

















###### References
- [Cyclic Number more info.](https://colinseymour.co.uk/142857-what-a-fascinating-number)
- [Planet Math](https://planetmath.org/cyclicnumber)
- [Universitet I Oslo: Lecture 8--Group Theory DH](https://www.uio.no/studier/emner/matnat/its/TEK4500/h20/lectures/lecture-8---group-theory-dh.pdf)
