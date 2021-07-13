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

**************
manage errors
**************
