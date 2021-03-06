###################################################################################
#
#	make fortran-tests
#		Compile and run example programs and test suite. Optional parameters 
#       should be identical to those used to make "all".
#
#   make python-tests
#		Run all python tests
#
#   OPTIONAL PARAMETER
#
#       F95     = name of F95 compiler (default gfortran)
#       LIBPATH = path to the libSHTOOLS.a archive (default ../../lib)
#       MODPATH = path to the SHTOOLS compiled modules (default ../../modules)
#       PYTHON  = name (including path) of Python (default python)
#
#	Written by Mark Wieczorek (March 2015).
#
#####################################################################################

VERSION = 3.0

F95 = gfortran
PYTHON = python

FFTW = -lfftw3
LAPACK = -llapack 
BLAS = -lblas

SHELL  = /bin/tcsh
MAKE   = make
LIBPATH = ../../lib
MODPATH = ../../modules
FEXDIR = fortran
PEXDIR = python


.PHONY: fortran-tests run-python-tests clean-fortran-tests clean-python-tests

getflags:
ifeq ($(F95),f95)
# Default Absoft Pro Fortran flags
F95FLAGS ?= -m64 -O3 -YEXT_NAMES=LCS -YEXT_SFX=_ -fpic
#-march=host
endif

ifeq ($(F95),gfortran)
# Default gfortran flags
#F95FLAGS ?= -m64 -fPIC -O3 # -march=native
F95FLAGS ?= -m64 -fPIC -O3 # -march=native  # -ggdb
endif

ifeq ($(F95),ifort)
# Default intel fortran flags
F95FLAGS ?= -m64 -free -O3 -Tf
endif

ifeq ($(F95),g95)
# Default g95 flags.
F95FLAGS ?= -O3 -fno-second-underscore 
endif

ifeq ($(F95),pgf90)
# Default pgf90 flags
F95FLAGS ?= -fast 
endif

ifeq ($(origin F95FLAGS), undefined)
F95FLAGS = -m64 -O3
endif


fortran-tests: getflags
	$(MAKE) -C $(FEXDIR) -f Makefile all F95=$(F95) F95FLAGS="$(F95FLAGS)" MODPATH=$(MODPATH) LIBPATH=$(LIBPATH) FFTW=$(FFTW) LAPACK=$(LAPACK) BLAS=$(BLAS)
	@echo
	@echo MAKE OF FORTRAN TEST SUITE SUCCESSFUL
	@echo
	$(MAKE) -C $(FEXDIR) -f Makefile run-fortran-tests
	@echo
	@echo RAN ALL FORTRAN EXAMPLE AND TESTS

run-fortran-tests:
	$(MAKE) -C $(FEXDIR) -f Makefile run-fortran-tests
	@echo
	@echo RAN ALL FORTRAN EXAMPLE AND TESTS

clean-fortran-tests:
	$(MAKE) -C $(FEXDIR) -f Makefile clean
	@echo
	@echo REMOVED FORTRAN TEST SUITE EXECUTABLES AND FILES

python-tests:
	$(MAKE) -C $(PEXDIR) -f Makefile all PYTHON=$(PYTHON)
	@echo
	@echo RAN ALL PYTHON TESTS

clean-python-tests:
	$(MAKE) -C $(PEXDIR) -f Makefile clean
	@echo
	@echo REMOVED PYTHON TEST SUITE EXECUTABLES AND FILES
