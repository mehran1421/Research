======================
**Things I Need to Know**
======================

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
