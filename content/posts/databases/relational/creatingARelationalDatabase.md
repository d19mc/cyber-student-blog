---
title: "Relational Databases: [01] Creating a Relational Database"
date: 2021-07-20T16:29:53-04:00
draft: true
tags:
    - Relational Databases
    - MySQL
---

# Preface

Even though I've always found data interesting, I never thought about it until I tried learning distributed hash tables. I wasn't able to grasp the concept; so here I am, learning it all from scratch.

I hope that by the end of this post, you'll understand the structure of the database and what the SQL Queries do when you execute them. 

![Image of a hard drive](sexyHardDrive.jpg)

## Prerequisites

- A machine with MySQL installed

## Why MySQL?

MySQL is the most popular RDBMS (relational database management system) developed by Oracle. There is a link in the references if you're not satisfied with this reason.

# Creating the Relational Database 

```sql
CREATE DATABASE db CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'usr'@'*' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'usr'@'*';
```


















###### References

**Why MySQL?**
- [Software Testing Help](https://www.softwaretestinghelp.com/what-is-mysql/) 
**How To Create a Database**
- [Ivan Borshchov](https://hinty.io/devforth/how-to-create-a-database-in-mysql-cli/)

