cmake_minimum_required(VERSION 3.20)
project(core LANGUAGES CXX)

# 1) Убедимся, что используем C++20
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# 2) Найдём внешние библиотеки
find_package(Boost REQUIRED COMPONENTS graph)            # Boost.Graph + алгоритмы из STL (Boost.Algorithm встроен)
find_package(spdlog REQUIRED)                           # логирование
find_package(nlohmann_json REQUIRED)                    # парсинг/сериализация JSON
# GoogleTest обычно подключают в tests/, а не в core. Его мы не тащим сюда.

# 3) Собираем сам core
add_library(core STATIC
  src/PipelineManager.cpp
  src/Scheduler.cpp
  src/GraphUtils.cpp
)

# 4) Include path, чтобы «apps» и «tests» видели наш хедер
target_include_directories(core
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# 5) Линкуем зависимости
target_link_libraries(core
  PUBLIC
    Boost::graph
    spdlog::spdlog
    nlohmann_json::nlohmann_json
)

# 6) Включаем C++20 и предупреждения
target_compile_features(core PUBLIC cxx_std_20)
target_compile_options(core PUBLIC
  $<$<CXX_COMPILER_ID:MSVC>:/W4>
  $<$<NOT:$<CXX_COMPILER_ID:MSVC>>:-Wall -Wextra -Wpedantic>
)
