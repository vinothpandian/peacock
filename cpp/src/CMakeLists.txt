cmake_minimum_required( VERSION 3.5 )
project( peacock )

set( CMAKE_CXX_STANDARD 11 )
set( CMAKE_CXX_EXTENSIONS OFF )

file( GLOB SOURCE_FILES *.cpp *.hpp )
add_executable( peacock ${SOURCE_FILES} )

find_package( ImageMagick COMPONENTS Magick++ REQUIRED )
add_definitions( -DMAGICKCORE_QUANTUM_DEPTH=16 )
add_definitions( -DMAGICKCORE_HDRI_ENABLE=1 )
include_directories( ${ImageMagick_INCLUDE_DIRS} )

find_package(Boost COMPONENTS system filesystem REQUIRED)

target_link_libraries( peacock ${ImageMagick_LIBRARIES} )
target_link_libraries( peacock 
  ${Boost_FILESYSTEM_LIBRARY}
  ${Boost_SYSTEM_LIBRARY}
)
