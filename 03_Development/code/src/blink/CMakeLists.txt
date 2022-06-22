# Blink example for compilation - Thnks yunkya2

add_executable(blink
        blink.c
)

target_link_libraries(blink pico_stdlib freertos)
pico_add_extra_outputs(blink)

pico_enable_stdio_usb(blink 1)
