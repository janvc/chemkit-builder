find_package(Chemkit COMPONENTS io md graphics gui REQUIRED)
include_directories(${CHEMKIT_INCLUDE_DIRS})

find_package(Boost COMPONENTS system filesystem iostreams REQUIRED)
include_directories(${Boost_INCLUDE_DIRS})

find_package(Qt5 COMPONENTS Widgets OpenGL LinguistTools REQUIRED)
include_directories(${Qt5Widgets_INCLUDE_DIRS})
include_directories(${Qt5OpenGL_INCLUDE_DIRS})

set(CMAKE_AUTOMOC ON)

include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(SOURCES
  builder.cpp
  buildertool.cpp
  builderwindow.cpp
  buildtool.cpp
  displaysettingsdock.cpp
  energyminimizationdock.cpp
  energyminimizer.cpp
  manipulatetool.cpp
  moleculelistdock.cpp
  moleculepropertiesdialog.cpp
  navigatetool.cpp
  toolsettingsdock.cpp
)

set(MOC_HEADERS
  builderwindow.h
  buildtool.h
  displaysettingsdock.h
  energyminimizationdock.h
  energyminimizer.h
  moleculelistdock.h
  moleculepropertiesdialog.h
  toolsettingsdock.h
)

set(UI_FORMS
  builderwindow.ui
  displaysettingsdock.ui
  energyminimizationdock.ui
  moleculelistdock.ui
  moleculepropertiesdialog.ui
  toolsettingsdock.ui
)

qt5_wrap_ui(UI_SOURCES ${UI_FORMS})
qt5_add_resources(RCC_SOURCES ${RESOURCES})

add_executable(chemkit-builder ${SOURCES} ${UI_SOURCES} ${RCC_SOURCES})
target_link_libraries(chemkit-builder Qt5::Widgets Qt5::OpenGL ${CHEMKIT_LIBRARIES} ${Boost_LIBRARIES})
install(TARGETS chemkit-builder DESTINATION bin)
