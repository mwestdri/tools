# This file is named "makefile.sample".
# Rename it "makefile".
# http://www.gnu.org/software/make/

FILES :=                              \
    .gitignore                        \
    .travis.yml                       \
    collatz-tests/mw23845-RunCollatz.in   \
    collatz-tests/mw23845-RunCollatz.out  \
    collatz-tests/mw23845-TestCollatz.py  \
    collatz-tests/mw23845-TestCollatz.out \
    Collatz.html                      \
    Collatz.log                       \
    Collatz.py                        \
    RunCollatz.py                     \
    RunCollatz.in                     \
    RunCollatz.out                    \
    TestCollatz.py                    \
    TestCollatz.out

all:

check:
	@echo "\nFiles found:\n=================================="
	@for i in $(FILES);                                         \
	do                                                          \
		[ -e $$i ] && echo "$$i"; \
	done
	@echo "\n*********************"
	@echo "* Files NOT FOUND:  *"
	@echo "*********************"
	@echo "=================================="
	@for i in $(FILES);                                         \
	do                                                          \
		[ -e $$i ] || echo "$$i"; \
	done
	@echo ""

clean:
	rm -f .coverage
	rm -f *.pyc
	rm -f Collatz.html
	rm -f Collatz.log
	rm -f RunCollatz.out
	rm -f TestCollatz.out
	rm -rf __pycache__

config:
	git config -l

sync:
	make clean
	@echo `pwd`
	@rsync -r -t -u -v --delete \
    --include "*.in"            \
    --include "*.py"            \
    --include "makefile"        \
    --exclude "*"               \
    . downing@$(CS):cs/cs373/github/python/projects/collatz/

test: RunCollatz.out TestCollatz.out

collatz-tests:
	git clone https://github.com/cs373-summer-2015/collatz-tests.git

Collatz.html: Collatz.py
	pydoc3 -w Collatz

Collatz.log:
	git log > Collatz.log

RunCollatz.out: RunCollatz.py
	./RunCollatz.py < RunCollatz.in > RunCollatz.out

TestCollatz.out: TestCollatz.py
	coverage3 run    --branch TestCollatz.py >  TestCollatz.out 2>&1
	coverage3 report -m                      >> TestCollatz.out
