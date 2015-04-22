list(APPEND alpscore_components hdf5 mc utilities)

foreach (comp ${alpscore_components})
    add_subdirectory(${comp})
endforeach(comp)
