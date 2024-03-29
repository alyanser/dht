cmake_minimum_required(VERSION 3.5)

project(RN-Praxis)

set(CMAKE_C_STANDARD 11)


add_executable(webserver
	src/webserver.c
	src/http.c
	src/util.c
	src/data.c
	src/dht.c
)


target_include_directories(webserver PRIVATE "include")

target_compile_options(webserver PRIVATE -Wall -Wextra -Wpedantic -Wno-infinite-recursion)

find_package(OpenSSL REQUIRED)
target_link_libraries(webserver PRIVATE ${OPENSSL_LIBRARIES} -lm)

find_package(Threads REQUIRED)
target_link_libraries(webserver PRIVATE Threads::Threads)

# Packaging
set(CPACK_SOURCE_GENERATOR "TGZ")

set(CPACK_SOURCE_IGNORE_FILES
	${CMAKE_BINARY_DIR}
	/\\..*$
)

set(CPACK_VERBATIM_VARIABLES YES)

include(CPack)
