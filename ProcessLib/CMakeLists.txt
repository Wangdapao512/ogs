include(${PROJECT_SOURCE_DIR}/scripts/cmake/OGSEnabledElements.cmake)

# Source files
APPEND_SOURCE_FILES(SOURCES)

add_subdirectory(BoundaryCondition)
APPEND_SOURCE_FILES(SOURCES BoundaryCondition)

add_subdirectory(Parameter)
APPEND_SOURCE_FILES(SOURCES Parameter)

add_subdirectory(GroundwaterFlow)
APPEND_SOURCE_FILES(SOURCES GroundwaterFlow)

add_subdirectory(TES)
APPEND_SOURCE_FILES(SOURCES TES)

APPEND_SOURCE_FILES(SOURCES Utils)

add_library(ProcessLib ${SOURCES})

target_link_libraries(ProcessLib
    MaterialLib
    MeshGeoToolsLib
    NumLib # for shape matrices
    ${VTK_LIBRARIES}
)

ADD_VTK_DEPENDENCY(ProcessLib)

if(TARGET Eigen)
    add_dependencies(ProcessLib Eigen)
endif()
if(TARGET Boost)
    add_dependencies(ProcessLib Boost)
endif()
