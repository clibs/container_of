Name
----

container_of - obtain a pointer to the struct that contains the struct member

Synopsis
--------

#include "container_of.h"

container_of(member_pointer, containing_struct, struct_member);

Description
-----------

The container_of() macro returns a pointer to the struct that contains this struct member.

This is useful if you have an API that passes a pointer to only the struct member. You can use this macro to obtain a pointer to the struct that contains that pointer.

*member_pointer* is a pointer to a member of *container_struct*. *container_struct* is the type of the struct that contains the member. *struct_member* is the literal of the member's name within *container_struct*.

Return Value
------------
A pointer to the struct that contains this member.

Example
-------

.. code-block:: c

    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include "container_of.h"

    typedef struct {
        char* name;
        int cash;
    } account_t;

    void deposit(int* current_balance, int change)
    {
        account_t* acc = container_of(current_balance, account_t, cash);
        printf("Increased %s's account by %d\n", acc->name, change);
    }

    int main()
    {
        account_t *acc = calloc(1, sizeof(account_t));
        acc->name = strdup("Alice");
        deposit(&acc->cash, 100);
    }

Further reading
---------------
http://broken.build/2012/11/10/magical-container_of-macro/
http://stackoverflow.com/questions/15832301/understanding-container-of-macro-in-linux-kernel
http://www.linuxjournal.com/files/linuxjournal.com/linuxjournal/articles/067/6717/6717s2.html
http://www.kroah.com/log/linux/container_of.html
http://en.wikipedia.org/wiki/Offsetof
