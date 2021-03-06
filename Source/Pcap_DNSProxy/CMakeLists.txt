# This code is part of Pcap_DNSProxy
# A local DNS server based on WinPcap and LibPcap
# Copyright (C) 2012-2015 Chengr28
# 
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either
# version 2 of the License, or (at your option) any later version.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.


# CMake minimum version
cmake_minimum_required(VERSION 3.0.2)

# Project name
project(Pcap_DNSProxy)

# Release version
set(CMAKE_BUILD_TYPE "Release")

# All source files
set(MAIN_SRC_FILES 
		"Base.h"
		"Capture.h"
		"Configuration.h"
		"DNSCurve.h"
		"Initialization.h"
		"Main.h"
		"Monitor.h"
		"Network.h"
		"PrintLog.h"
		"Process.h"
		"Protocol.h"
		"Base.cpp"
		"Capture.cpp"
		"Configuration.cpp"
		"DNSCurve.cpp"
		"Initialization.cpp"
		"Main.cpp"
		"Monitor.cpp"
		"Network.cpp"
		"PrintLog.cpp"
		"Process.cpp"
		"Protocol.cpp")

# Compiling and linking flags
add_definitions(-std=c++11 -fpic)
IF(ENABLE_PCAP)
	add_definitions(-DENABLE_PCAP)
ENDIF(ENABLE_PCAP)
IF(ENABLE_LIBSODIUM)
	add_definitions(-DENABLE_LIBSODIUM)
ENDIF(ENABLE_LIBSODIUM)

# Executable file name
add_executable(Pcap_DNSProxy ${MAIN_SRC_FILES})

# Static libraries
target_link_libraries(Pcap_DNSProxy pthread)
IF(ENABLE_PCAP)
	target_link_libraries(Pcap_DNSProxy pcap)
ENDIF(ENABLE_PCAP)
IF(ENABLE_LIBSODIUM)
	target_link_libraries(Pcap_DNSProxy sodium)
ENDIF(ENABLE_LIBSODIUM)
