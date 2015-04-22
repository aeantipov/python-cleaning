# sample CMake to build a python interface to an alpscore module
set(comp hdf5)
set(lib_name py${comp}_c)
set(comp_files 
    pyhdf5.cpp
)
#set(deps pyutilities_c)
set(extra_files ../utilities/import_numpy.cpp)

include_directories(${PYTHON_INCLUDE_DIRS})
add_library(${lib_name} MODULE ${comp_files} ${extra_files})

foreach(dep ${deps}) 
    target_link_libraries(${lib_name} ${dep})
endforeach(${dep})


set_target_properties(${lib_name} PROPERTIES COMPILE_DEFINITIONS "${ALPS_SHARED_CPPFLAGS}")
set_target_properties(${lib_name} PROPERTIES PREFIX "")
target_link_libraries(${lib_name} ${PYTHON_LIBRARIES} ${LINK_ALL})

install(TARGETS ${lib_name} DESTINATION python)

