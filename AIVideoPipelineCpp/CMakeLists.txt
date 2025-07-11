cmake_minimum_required(VERSION 3.20)
project(AIVideoPipelineCpp LANGUAGES CXX)

# 1) Включаем C++20
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# 2) Единая папка для всех exe (для мультиконфиг-генераторов VS)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
foreach(cfg IN ITEMS Debug Release RelWithDebInfo MinSizeRel)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${cfg} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})
endforeach()

# 3) Покажем пути, если пригодится
message(STATUS "Source dir: ${CMAKE_SOURCE_DIR}")
message(STATUS "Binary dir: ${CMAKE_BINARY_DIR}")

# 4) Добавляем подпроекты
add_subdirectory(apps/api_server)
# в будущем сюда же можно добавить:
# add_subdirectory(apps/broker_worker)
# add_subdirectory(apps/db_migrator)
# add_subdirectory(apps/video_pipeline)
# и, когда будут готовы, libs:
# add_subdirectory(libs/core)
# add_subdirectory(libs/tasks)
# add_subdirectory(libs/utils)
