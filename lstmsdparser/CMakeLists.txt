include_directories (${PROJECT_SOURCE_DIR}/)

set (lstm_sdparser_VERSION "0.0.1")
set (lstm_sdparser_SRC
    lstm_sdparser.cpp
    )

add_library(lstm_sdparser_static_lib STATIC lstm_sdparser_dll.cpp ${lstm_sdparser_SRC})
set_target_properties (lstm_sdparser_static_lib    PROPERTIES
    OUTPUT_NAME     lstm_sdparser)

add_library(lstm_sdparser_shared_lib SHARED lstm_sdparser_dll.cpp ${lstm_sdparser_SRC})
set_target_properties (lstm_sdparser_shared_lib    PROPERTIES
    VERSION         ${lstm_sdparser_VERSION}
    OUTPUT_NAME     lstm_sdparser)

# redirect output binary to tools/train
add_executable(lstmparse main.cpp ${lstm_sdparser_SRC})
target_link_libraries(lstmparse cnn ${Boost_LIBRARIES})

add_executable(lstm_par_cmdline lstm_par_cmdline.cpp)
target_link_libraries (lstm_par_cmdline lstm_sdparser_static_lib cnn ${Boost_LIBRARIES})


