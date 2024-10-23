if(DEFINED ESP_PLATFORM)
    idf_component_register(SRCS
                        "src/pb_common.c"
                        "src/pb_encode.c"
                        "src/pb_decode.c"
                        INCLUDE_DIRS "include"
                        )
endif()