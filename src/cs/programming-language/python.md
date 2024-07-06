# Python

Functional Programming is stateless.

Object Oriented Programming is stateful.


## Typed Python
If the function has no return, using -> None in return is recommended

```python
def foo() -> None:
	print("hello")

```

For error handling functions, use NoReturn
```python
def error() -> NoReturn:
	raise ValueError
```