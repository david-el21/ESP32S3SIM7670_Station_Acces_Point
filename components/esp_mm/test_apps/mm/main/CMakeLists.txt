set(srcs "test_app_main.c")

list(APPEND srcs "test_mmap.c")

if(CONFIG_SOC_CACHE_WRITEBACK_SUPPORTED)
    list(APPEND srcs "test_cache_msync.c")
endif()

if(CONFIG_SOC_CACHE_FREEZE_SUPPORTED)
    list(APPEND srcs "test_cache_utils.c")
endif()

# In order for the cases defined by `TEST_CASE` to be linked into the final elf,
# the component can be registered as WHOLE_ARCHIVE
idf_component_register(SRCS ${srcs}
                       PRIV_REQUIRES unity esp_partition spi_flash esp_mm driver esp_timer test_mm_utils test_utils
                       WHOLE_ARCHIVE)
