#
# Copyright (c) 2019 -2021 MINRES Technolgies GmbH
#
# SPDX-License-Identifier: Apache-2.0
#
cmake_minimum_required(VERSION 3.12)

project(tgc-vp LANGUAGES C CXX VERSION 0.0.1)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/etiss-sc/cmake/)

set(ETISS_SC_SRC "${CMAKE_SOURCE_DIR}/etiss-sc/src/")

find_package(Boost COMPONENTS program_options thread REQUIRED)
find_package(ETISS REQUIRED)
###############################################################################
# SiFive
###############################################################################
add_executable(${PROJECT_NAME}
	sc_main.cpp
	CLIParser.cpp
	tgc_vp/tb.cpp
	tgc_vp/system.cpp

	${ETISS_SC_SRC}/utils/config.cpp
	${ETISS_SC_SRC}/utils/plugins.cpp
	${ETISS_SC_SRC}/utils/logging.cpp
	${ETISS_SC_SRC}/tlm/generic/cpu_minres.cpp
)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_LIST_DIR} ${CMAKE_SOURCE_DIR}/etiss-sc/include/)
target_link_libraries(${PROJECT_NAME} PUBLIC dbt-rise-tgc_sc vpvper_generic vpvper_sifive ${BOOST_program_options_LIBRARY} ETISS::etiss)
if(TARGET Boost::program_options)
	target_link_libraries(${PROJECT_NAME} PUBLIC Boost::program_options Boost::thread)
else()
	target_link_libraries(${PROJECT_NAME} PUBLIC ${BOOST_program_options_LIBRARY})
endif()
