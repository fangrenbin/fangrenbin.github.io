---
author: fangrenbin
comments: true
date: 2012-06-15 10:20:02+00:00
layout: post
slug: sortarraylist
title: SortArrayList
wordpress_id: 368
categories:
- Java
---


    package com.knet;
    
    class Student implements Comparable{
        private String name;
        private int age;
        private double score;
        
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public int getAge() {
            return age;
        }
        public void setAge(int age) {
            this.age = age;
        }
        public double getScore() {
            return score;
        }
        public void setScore(double score) {
            this.score = score;
        }
    
        public Student(String s, int i, double d) {
            // TODO Auto-generated constructor stub
            this.name=s;
            this.age=i;
            this.score=d;
        }
        public String toString(){
            return "[Student]"+"name:"+name+"age:"+age+"score:"+score;
        }
        public int compareTo(Object o) {
            // TODO Auto-generated method stub
            Student s=(Student)o;
            return (int) (s.getScore()-this.getScore());
        }
    }
    
    
