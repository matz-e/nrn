npylib = libnrnpython@npy_pyver10@
lib_LTLIBRARIES = libnrnpython@npy_pyver10@.la librxdmath.la


nsrc=$(top_srcdir)/src
DEFS = @DEFS@ @NRNPYTHON_DEFINES@
NRNPYTHON_INCLUDES = @npy_NRNPYTHON_INCLUDES@
IV_INCLUDES = @IV_INCLUDE@ $(X_CFLAGS)
includes =  -I. -I$(nsrc)/nrniv -I$(nsrc)/ivoc -I$(nsrc)/nrnoc -I$(nsrc)/oc -I$(nsrc)/nrnmpi -I$(nsrc)/gnu -I$(nsrc)/mesch $(NRNPYTHON_INCLUDES) $(IV_INCLUDES)
AM_CPPFLAGS = -DOOP=1 -DCABLE=1 -DUSECVODE=1 -DUSEMATRIX=1 -DUSEBBS=1 $(includes)
AM_CXXFLAGS = @MINGW_CFLAG@

if BUILD_NRNPYTHON
if BUILD_CYGWIN
EXTEND = inithoc.cpp
else
if BUILD_MINGW
EXTEND = inithoc.cpp
else
EXTEND =
endif
endif
endif

libnrnpython@npy_pyver10@_la_SOURCES = nrnpython.cpp nrnpy_hoc.cpp nrnpy_nrn.cpp \
	nrnpy_p2h.cpp grids.cpp rxd.cpp rxd_extracellular.cpp rxd_intracellular.cpp rxd_vol.cpp rxd_marching_cubes.c rxd_llgramarea.c $(EXTEND)

librxdmath_la_SOURCES = rxdmath.c $(EXTEND)

noinst_HEADERS = nrnpython.h nrnwrap_Python.h nrnpy_reg.h \
	nrnpy_hoc_2.h nrnpy_hoc_3.h \
	nrnpy_nrn_2.h nrnpy_nrn_3.h hoccontext.h \
	nrnpy_utils.h rxd.h grids.h

if BUILD_MINGW
nrnpython.dll: $(npylib).la
	$(CC) -shared -Wl,--out-implib,$(npylib).dll.a \
	  -o nrnpython.dll .libs/*.o
endif

if BUILD_NRNPYTHON
BUILT_SOURCES = force setup.py
force:
	if test inithoc.cpp -ot $(nsrc)/nrnpython/inithoc.cpp ; then \
		cp $(nsrc)/nrnpython/inithoc.cpp inithoc.cpp ; \
	fi

clean-local:
	-rm -rf build

endif
