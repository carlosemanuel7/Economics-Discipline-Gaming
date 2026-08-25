cmake_minimum_required(VERSION 3.20)
project(MeuJogo CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Ajuda o VS Code a ler os arquivos e tirar as linhas vermelhas
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# --- A LINHA MÁGICA QUE CORRIGE O ERRO ---
# Avisa o godot-cpp que estamos usando a API da versão 4.7
set(GODOTCPP_API_VERSION "4.7" CACHE STRING "Godot API version")

# Inclui os binds da Godot
add_subdirectory(godot-cpp)

# Pega todos os arquivos da pasta src
file(GLOB_RECURSE SOURCES "src/*.cpp")
file(GLOB_RECURSE HEADERS "src/*.h" "src/*.hpp")

# Cria a biblioteca dinâmica
add_library(meujogo SHARED ${SOURCES} ${HEADERS})
target_link_libraries(meujogo godot-cpp)

# Joga o arquivo compilado dentro do projeto da Godot
set_target_properties(meujogo PROPERTIES 
    PREFIX "lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/game/bin"
)