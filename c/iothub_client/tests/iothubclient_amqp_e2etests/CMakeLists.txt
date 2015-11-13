#Copyright (c) Microsoft. All rights reserved.
#Licensed under the MIT license. See LICENSE file in the project root for full license information.

#this is CMakeLists.txt for iothubclient_amqp_e2etests
cmake_minimum_required(VERSION 3.0)

if(NOT (${use_amqp}))
	message(FATAL_ERROR "iothubclient_amqp_e2etests being generated without AMQP support")
endif()

compileAsC99()
set(theseTestsName iothubclient_amqp_e2etests)

set(${theseTestsName}_cpp_files
	${theseTestsName}.cpp
)

set(${theseTestsName}_c_files
)

set(${theseTestsName}_h_files
)

include_directories(${IOTHUB_TEST_INC_FOLDER})

build_test_artifacts(${theseTestsName} ON)




if(WIN32)
	if(TARGET ${theseTestsName}_dll)
		target_link_libraries(${theseTestsName}_dll
			iothub_test
			iothub_client
			iothub_client_amqp_transport
			common
		)
		linkProton(${theseTestsName}_dll)
	endif()
	
	if(TARGET ${theseTestsName}_exe)
		target_link_libraries(${theseTestsName}_exe
			iothub_test
			iothub_client
			iothub_client_amqp_transport
			common
		)
		linkProton(${theseTestsName}_exe)	
	endif()
else()
	if(TARGET ${theseTestsName}_exe)
		target_link_libraries(${theseTestsName}_exe
			iothub_test
			iothub_client
			iothub_client_amqp_transport
			common
		)
		target_link_libraries(${theseTestsName}_exe pthread)
		linkProton(${theseTestsName}_exe)
	endif()
endif()
