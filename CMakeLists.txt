# CMakeLists.txt for QGpgME
# Copyright 2025 g10 Code GmbH
# Software engineering by Carl Schwan <carl.schwan@gnupg.com>
# Software engineering by Ingo Klöcker <dev@ingo-kloecker.de>
#
# This file is part of QGpgME, the Qt API binding for GpgME.
#
# QGpgME is free software; you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# QGpgME is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, see <https://gnu.org/licenses/>.
# SPDX-License-Identifier: GPL-2.0-or-later

cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

set(FULL_VERSION "2.0.0")

string(REGEX MATCH "^[0-9]+.[0-9]+.[0-9]+" cmake_compat_version ${FULL_VERSION})
project(qgpgme VERSION ${cmake_compat_version})

set(VERSION_MAJOR ${PROJECT_VERSION_MAJOR})
set(VERSION_MINOR ${PROJECT_VERSION_MINOR})
set(VERSION_MICRO ${PROJECT_VERSION_PATCH})

# LT Version numbers, remember to change them just *before* a release.
#   (Code changed:			REVISION++)
#   (Interfaces added/removed/changed:	CURRENT++, REVISION=0)
#   (Interfaces added:			AGE++)
#   (Interfaces removed:		AGE=0)
set(LIBQGPGME_LT_CURRENT "22")
set(LIBQGPGME_LT_AGE "7")
set(LIBQGPGME_LT_REVISION "0")
math(EXPR LIBQGPGME_SOVERSION "${LIBQGPGME_LT_CURRENT} - ${LIBQGPGME_LT_AGE}")

set(GPG_ERROR_REQUIRED_VERSION "1.47")
set(GPGME_REQUIRED_VERSION "1.24.2")
set(GPGMEPP_REQUIRED_VERSION "${VERSION_MAJOR}.${VERSION_MINOR}.0")
set(QT5_REQUIRED_VERSION "5.15.0")
set(QT6_REQUIRED_VERSION "6.5.0")

option(QGPGME_BUILD_QT5 "Build for Qt5" ON)
option(QGPGME_BUILD_QT6 "Build for Qt6" ON)

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules ${CMAKE_MODULE_PATH})

include(G10CMakeSettings)
include(G10CompilerSettings)
include(FeatureSummary)
include(GNUInstallDirs)

set(CMAKE_AUTOMOC ON)

find_package(LibGpgError ${GPG_ERROR_REQUIRED_VERSION})
set_package_properties(LibGpgError PROPERTIES TYPE REQUIRED)
find_package(Gpgme ${GPGME_REQUIRED_VERSION})
set_package_properties(Gpgme PROPERTIES TYPE REQUIRED)
find_package(Gpgmepp ${GPGMEPP_REQUIRED_VERSION} CONFIG)
set_package_properties(Gpgmepp PROPERTIES DESCRIPTION "GpgME++ library" URL "https://www.gnupg.org" TYPE REQUIRED)

if(QGPGME_BUILD_QT5)
    set(QT_MAJOR_VERSION 5)
    find_package(Qt5 ${QT5_REQUIRED_VERSION} REQUIRED COMPONENTS Core)
    add_subdirectory(src 5/src)
endif()

if(QGPGME_BUILD_QT6)
    set(QT_MAJOR_VERSION 6)
    find_package(Qt6 ${QT6_REQUIRED_VERSION} CONFIG REQUIRED Core CoreTools)
    add_subdirectory(src 6/src)
endif()

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
