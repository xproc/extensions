# pxf:cwd()

This function returns the “current working directory” of the
processor. This function takes no arguments and does not depend on the
context. This function should only be implemented by processors for
which the concept of a “current working directory” is coherent.

There are no standard XProc steps that change the working directory,
so this function is likely to return the same value every time it is
called. However, there is nothing which prevents an extension step
from being defined which changes the current working directory, so it
is not necessarily the case that the same value will always be
returned.
