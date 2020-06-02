Bug related to order of files passed on the command line:

Running `run1.sh`

`python3 -m pylint test2/test3/test.py test2/test4/test.py test/__init__.py`

```
************* Module test
test2/test3/test.py:2:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:3:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:4:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:5:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:6:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:2:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:3:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:4:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:5:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:6:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:2:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:3:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:4:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:5:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:6:2: W0104: Statement seems to have no effect (pointless-statement)
************* Module test.__init__
test/__init__.py:1:0: R0801: Similar lines in 2 files
==test:1
==test:1
  1
  2
  3
  4
  5 (duplicate-code)

--------------------------------------------------------------------
Your code has been rated at -3.33/10 (previous run: -3.33/10, +0.00)
```

in particular, this entry is incorrect:
```
test/__init__.py:1:0: R0801: Similar lines in 2 files
```

while running `run2.sh`

`python3 -m pylint test/__init__.py test2/test3/test.py test2/test4/test.py`

```
************* Module test
test2/test3/test.py:2:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:3:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:4:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:5:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test3/test.py:6:4: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:2:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:3:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:4:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:5:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:6:0: W0311: Bad indentation. Found 2 spaces, expected 4 (bad-indentation)
test2/test4/test.py:2:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:3:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:4:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:5:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:6:2: W0104: Statement seems to have no effect (pointless-statement)
test2/test4/test.py:1:0: R0801: Similar lines in 2 files
==test:1
==test:1
  1
  2
  3
  4
  5 (duplicate-code)

--------------------------------------------------------------------
Your code has been rated at -3.33/10 (previous run: -3.33/10, +0.00)
```

that is the expected output.
