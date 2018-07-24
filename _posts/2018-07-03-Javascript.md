---
layout: post
title: "Javascript"
date: 2018-07-05
excerpt: ""
tags:
- Language
comments: true
---
#### Basic Javascript
    // 변수
      var a, b;

    // 변수에 함수대입
      var c = function(){
        ...
      }

    // 함수(=객체)
      function func(){}
      func();
      // window 생략가능
      window.func();

    // 객체
      a = {}
      b = {
        a : 1,
        b : function(){
          alert('');
        }
      }

    // 인스턴스 생성
      a = new func();

    // 클로져

    // 함수 즉시호출
      (function func(){
        ...
      }())

    // 전역 객체의 함수호출
      window.func();


    // 객체의 함수
      instance.func();
      window.instance.func();
      ---> Instance.func 호출시 this == Instance


    // o1호출(전역)과 o2호출 차이
      function func(){}
      var o1 = func();
      var o2 = new func();


    // apply, call
      var o = {}
      var p = {}
      function func(){
          switch(this){
              case o:
                  document.write('o<br />');
                  break;
              case p:
                  document.write('p<br />');
                  break;
              case window:
                  document.write('window<br />');
                  break;          
          }
      }
      func();
      func.apply(o);
      func.apply(p);


    // 리터럴
      a = [1,2,3]
      a = new array(1,2,3)

      Function b(x, y) = { return x + y }
      b = new Function('x', 'y', 'return x+y')

      c = {}
      c = new Object()

    // 프로토타입
      // 모든 객체는 프로토타입이 존재
      function Person(name){
          this.name = name;
      }
      Person.prototype.name=null;
      Person.prototype.introduce = function(){
          return 'My name is '+this.name;
      }

      function Programmer(name){
          this.name = name;
      }
      Programmer.prototype = new Person();
      Programmer.prototype.coding = function(){
          return "hello world";
      }

      var p1 = new Programmer('egoing');
      document.write(p1.introduce()+"<br />");
      document.write(p1.coding()+"<br />");

      // 객체 함수 정의는 프로토 타입에(객체.prototype.함수 = function(){})
      // 객체 함수 호출은 객체.함수


#### ECMAScript2016
    // Class
      class Person {
          constructor (id, name) {
              this.id = id
              this.name = name
          }
          toString() {
              return `(${this.id}, ${this.name})`
          }
      }

      class Student extends Person {
          constructor (id, name, age) {
              super(id, name)
              this.age = age
          }
          toString() {
              return super.toString() + ' and ' + this.age
          }
      }

    // let&const
      const schoolName = "ABC"
      schoolName = "CBA"  // Error
      // 호이스팅이 사라짐
      function test() {
        let x = "a"
        if (true) {
          let x = "b"
          console.log(x);  // b
        }
        console.log(x);  // a
      }

    // Arrow Functions
      const squares = [1, 2, 3].map(x => x * x) // 1, 4, 9

      // this에 대한 이전코드
      function NumberEx() {
        var that = this
        that.num = 0;
        setInterval(function add() {
          // setInterval 안에서의 this 는 NumberEx의 this가 아니므로 다른 변수에 this 를 지정하여 씁니다.
          that.num++;
          console.log(that.num);
        }, 1000);
      }

      // this에 대한 바뀐코드
      function NumberEx() {
        this.num = 0

        setInterval(() => {
          this.num++ // this is from NumberEx
        }, 1000)
      }

    // module
      // utility.js
      export const squares = (arr) => { return arr.map(x => x * x) }

      // math.js
      import { squares } from "utility"
      console.log(squares([1,2,3])) // [1,4,9]


    // Promises
    var promiseTest = (num) => {
      return new Promise((resolve, reject) => {
          if (num > 3) {
              resolve(num)
          } else {
              reject("err")
          }
      }
    }

    promiseTest(5)
      .then(val => console.log(val)) // 5
      .catch(err => console.log(err))
