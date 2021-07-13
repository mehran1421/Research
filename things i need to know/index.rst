======================
**Things I Need to Know**
======================

.. contents:: Overview
   :depth: 3


*******************************
dont use Technical Debt(بدهی فنی)
*******************************
if we dont have enough time for project and we do work that Make writing code fast
The advice is to never sacrifice quality for speed because You will have to spend 30% more time later to refactor the code

**************************
use Functional Programing
**************************
the way that The logic used in the program is considered as mathematical functions

We assign specific responsibilities to each function

The advantage is that we can easily debug the program

********************
write standard code
********************
there is a write Code rules in each program Language that Makes the written program more readable

for example there is **PEP-8** in *python*

- use 4 spaces per indentation level
- separate top-level function and class definitions with two blank lines
- method definitions inside a class are separated by a single blank line
- use space after and before '='.

.. code:: python

    from .models import (
        Product,
        Category,
        FigureField,
    )


    class ProductViews(ViewSet):
        lookup_field = 'slug'

        def list(self, request):
            """
            for superuser return all object and
            for other user return Objects that status=True,choice='p'
            :param request:
            :return:
            """
            if request.user.is_superuser:
                product = Product.objects.all()
            else:
                product = Product.objects.filter(status=True, choice='p')
            serializer = ProductSerializer(product, context={'request': request}, many=True)
            return Response(serializer.data)

****************
Beautiful code
****************
Code that is simply written, Different sections such as classes, functions, variables are well named
So that if see another programmer it, Understands the task of the code easily

*************
Refactoring
*************
One of the main topics in software engineering references, there are two factor for **Refactoring**

- How much time does it take us?
- Cost spent
For example, maybe writen program and Refactor it Improves program performance.

We must use the previous code as much as possible Because Months of effort are wasted.

Per change code, we must Test program

***************
Work conscience
***************
A good programmer is someone who have **work conscience**. that's mean Whatever program he gets, he will do his best to improve the code.

**************************
Software engineering tools
**************************
Do not have a bias in the programming language

for example, **face book**, the first development program with PHP but After, making a lot of money change, created his own programming language(HACK)

**********************************************************
write Dictionary for code and use good name for variable
**********************************************************
An important factor in software quality is the existence of a dictionary of functions, classes and variables

Let's try to choose meaningful names for the variables, In this case, the code we wrote will be of better quality

***********
Commenting
***********

**Header Comments**
    We must comment on the following at the top of each file:
        + programmer name
        + date program
        + file name
        + Names of other files that are associated with this file
**Functions Comments**
    Each function has the task of doing something in the program:
        + What is the function supposed to do?
        + what is parameter
        + what is return
**Inline Comments**
    descriptions the code in one line

*************
Reusable
*************
Reuse previously written code

- **Advantages**
    + Reduces coding time
    + Reduce potential bugs in the program
    + Reduction in costs

- **Disadvantages**
    + If written by another programmer, We must pay attention to the issue of security
    + Dependence between codes increases

************************
Short code with function
************************
we must Divide code into smaller sections, Even the **devil's Advocate** can not object

.. note::
    Devils Advocate that means Someone who sees all the flaws in the code

- dont use functions that are GOTO in nature
- dont use **GLOBAl VARIABLE** in code Because can change it
- better than Defining variable into functions
- use Indentation in code for More readability for example

.. code:: python

    from django.http import HttpResponseForbidden
    from admin_honeypot.models import LoginAttempt


    class BlockedIpMiddleware(object):

        def __init__(self, get_response):
            self.get_response = get_response

        def __call__(self, request):
            for i in LoginAttempt.objects.all():
                if request.META['REMOTE_ADDR'] in i.ip_address:
                    return HttpResponseForbidden('<h1>Forbidden</h1>')
            response = self.get_response(request)
            return response

- use Meaningful names for variable that dont need to commenting
- if there is nested code in program, it is better to write functions for per nested cod
- per functions just do one work and Avoid for super functions(Jack of all trades)
- your code must Be limited parameter (Maximum 3)

******************
real data for test
******************
use real data for test for example dont use for username = ali1,ali2,...

************
type errors
************
- **software errors**
    + return empty object or things
    + dont manage exception in try-except

*******
DRY
*******
DRY(Dont Repeat Yourself- دوباره کاری نکن) is one of the most basic rules of programming,

The programmer must know which part of the program is duplicate and try that Reduce duplicate code by functions or class ,...

if you use DRY, you can Refactoring code later

In general, using dry can write code with more basic, simple programs and better quality

**********************************
Know what we are going to commit to
**********************************
there are two programmer when ask questions that "what are you doing?": programmer says
- I'm working on a user-related class
    + he know that what to commit
    + he know that what are doing and know that What part of the program has its coding improved
    + he can return back with Ctrl+z
- In an effort to improve the service of users
    + he dont know that when finish work and what to commit

**************************
Make our code transparent
**************************
- **write document project**
    Commenting is essential for important parts of the software
- **Testing**
    tests help developer that Get acquainted with different parts of the project and if change it If you change part of the project, let us know what other parts of the project to change

********************************************
Introduction to Concurrency and Parallelism
********************************************
- Concurrency

    two or more that They start and run simultaneously
- Parallelism

    if many task that Simultaneously handled by a multi-core processor

.. note::
    Concurrency Are related to the implementation of separate processes

    but Parallelism Simultaneous implementation of related tasks

*************
SOLID
*************

- Single Responsibility Principle
    A class must do a task and all functions into class must work on the same goal
- Open/Close Principle
    Never change the previous class and write the new code in a new class And we inherit from the previous class
- Liskov Substitution Principle
    کلاس فرزند باید بتواند تمام ویژگی های کلاس پدر را انجام دهد. اگر به طور مثال بگوییم که همه ی کار های والد را انجام میدهد به جز یک کار آن وقت این اصل را نقص کردیم
- Interface Segregation Principle
    حتما از اینترفیس ها استفاده کنیم: اینترفیس ها هما کلاس هایی هستند که تمام متدهای کلاس ما را تشریح میکنند و مشخص میکنند که برای اجرای این کلاس چه توابعی باید استفاده شود
- Dependency Inversion Principle
    کاهش وابستگی بین کلاس ها

