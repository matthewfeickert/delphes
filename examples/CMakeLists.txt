include_directories(
  ${CMAKE_SOURCE_DIR}
  ${ROOT_INCLUDE_DIRS}
  ${DelphesExternals_INCLUDE_DIR}
)

file(GLOB executables RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.cpp)
file(GLOB macros *.C *.tcl *.tfs)

# build all executables and put them into bin/
foreach(sourcefile ${executables})
  string(REPLACE ".cpp" "" name ${sourcefile})
  add_executable(${name} ${sourcefile})
  target_link_libraries(${name} Delphes)
  install(TARGETS ${name} DESTINATION bin)
endforeach()

# take all other relevant files and put them into examples/
install(FILES ${macros} DESTINATION examples)
install(DIRECTORY ExternalFastJet DESTINATION examples)
if(PYTHIA8_FOUND)
  install(DIRECTORY Pythia8 DESTINATION examples)
endif()
