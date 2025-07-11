# Имя проекта совпадает с корнем, чтобы exe носил единое имя
project(AIVideoPipelineCpp LANGUAGES CXX)

# Собираем наш простой стартап-экзешник
add_executable(AIVideoPipelineCpp
    main.cpp
)

# Подключение include-путей (если потребуется)
# target_include_directories(AIVideoPipelineCpp PRIVATE
#     ${CMAKE_SOURCE_DIR}/libs/core/include
#     ${CMAKE_SOURCE_DIR}/libs/utils/include
# )

# Линковка общих библиотек-пустышек (потом раскомментируешь)
# target_link_libraries(AIVideoPipelineCpp PRIVATE
#     core
#     tasks
#     utils
# )

# Жёсткие warning-флаги для повышения качества кода
target_compile_options(AIVideoPipelineCpp PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>:/W4 /permissive->
    $<$<CXX_COMPILER_ID:GNU,Clang>:-Wall -Wextra -Wpedantic>
)
