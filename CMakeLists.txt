cmake_minimum_required(VERSION 3.16)

project(ChessAnalyser LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(SFML 2.5 COMPONENTS graphics window system REQUIRED)

add_executable(ChessAnalyser
	main.cpp
	game.cpp
	piece.cpp
	chess.cpp
)

target_link_libraries(ChessAnalyser PRIVATE sfml-graphics sfml-window sfml-system)

# Copy runtime assets next to the executable.
add_custom_command(TARGET ChessAnalyser POST_BUILD
	COMMAND ${CMAKE_COMMAND} -E copy_directory
			${CMAKE_SOURCE_DIR}/images
			$<TARGET_FILE_DIR:ChessAnalyser>/images
)

add_custom_command(TARGET ChessAnalyser POST_BUILD
	COMMAND ${CMAKE_COMMAND} -E copy_if_different
			${CMAKE_SOURCE_DIR}/arial.ttf
			$<TARGET_FILE_DIR:ChessAnalyser>/arial.ttf
)