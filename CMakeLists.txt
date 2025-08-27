cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)

#============================================================================
# Initialize the project
#============================================================================
project(gz-jetty VERSION 1.0.0)

#============================================================================
# Find gz-cmake
#============================================================================
# If you get an error at this line, you need to install gz-cmake
find_package(gz-cmake REQUIRED)

#============================================================================
# Configure the project
#============================================================================
gz_configure_project(VERSION_SUFFIX pre1)

# all list of jetty packages

gz_find_package(gz-common REQUIRED)
gz_find_package(gz-fuel_tools REQUIRED)
gz_find_package(gz-sim REQUIRED)
gz_find_package(gz-gui REQUIRED)
gz_find_package(gz-launch REQUIRED)
gz_find_package(gz-math REQUIRED)
gz_find_package(gz-msgs REQUIRED)
gz_find_package(gz-physics REQUIRED)
gz_find_package(gz-plugin REQUIRED)
gz_find_package(gz-rendering REQUIRED)
gz_find_package(gz-sensors REQUIRED)
gz_find_package(gz-transport REQUIRED)
gz_find_package(gz-utils REQUIRED)
gz_find_package(sdformat REQUIRED)

if(build_warnings)
  set(all_warnings " CONFIGURATION WARNINGS:")
  foreach (msg ${build_warnings})
    gz_string_append(all_warnings " -- ${msg}" DELIM "\n")
  endforeach ()
  message(WARNING "${all_warnings}")
endif (build_warnings)

if(build_errors)
  message(SEND_ERROR "-- BUILD ERRORS: These must be resolved before compiling.")
  foreach(msg ${build_errors})
    message(SEND_ERROR "-- ${msg}")
  endforeach()
  message(SEND_ERROR "-- END BUILD ERRORS\n")

  set(error_str "Errors encountered in build. Please see BUILD ERRORS above.")

  message(FATAL_ERROR "${error_str}")

endif()

install(FILES release_notes.md  DESTINATION ${GZ_DATA_INSTALL_DIR})
