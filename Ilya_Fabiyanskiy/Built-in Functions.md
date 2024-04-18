all(_iterable_)[](https://docs.python.org/3/library/functions.html#all "Permalink to this definition")

Return `True` if all elements of the _iterable_ are true (or if the iterable is empty). Equivalent to:

def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True

