set(imgdecoder-gdip_header
    imgdecoder-gdip.h
)

set(imgdecoder-gdip_src
    imgdecoder-gdip.cpp
)

source_group("Header Files" FILES ${imgdecoder-gdip_header})
source_group("Source Files" FILES ${imgdecoder-gdip_src})

if (NOT ENABLE_SOUI_COM_LIB)
    set (imgdecoder-gdip_src  ${imgdecoder-gdip_src} imgdecoder-gdip.rc)
    add_library(imgdecoder-gdip SHARED ${imgdecoder-gdip_src} ${imgdecoder-gdip_header})
else()
    add_library(imgdecoder-gdip STATIC ${imgdecoder-gdip_src} ${imgdecoder-gdip_header})
    target_compile_definitions(imgdecoder-gdip
      PUBLIC SOUI_IMAGE_DECODER_USE_GDIPLUS_STATIC
    )
endif()

target_compile_definitions(imgdecoder-gdip
  PUBLIC SOUI_IMAGE_DECODER_USE_GDIPLUS
)
target_include_directories(imgdecoder-gdip
  PRIVATE ${PROJECT_SOURCE_DIR}/config
  PRIVATE ${PROJECT_SOURCE_DIR}/utilities/include
  PRIVATE ${PROJECT_SOURCE_DIR}/SOUI/include
  PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}
)

set(COM_LIBS ${COM_LIBS} imgdecoder-gdip CACHE INTERNAL "com_lib")
set_target_properties (imgdecoder-gdip PROPERTIES
    FOLDER components/imgdecoder
)
target_link_libraries(imgdecoder-gdip gdiplus.lib)