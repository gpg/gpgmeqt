# CMakeLists.txt for QGpgME
# Copyright 2021 Daniel Vrátil <dvratil@kde.org>
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

add_compile_definitions(BUILDING_QGPGME)
add_compile_definitions(GPG_ERR_SOURCE_DEFAULT=GPG_ERR_SOURCE_GPGME)
if(WIN32)
  add_compile_definitions(GPG_ERR_ENABLE_GETTEXT_MACROS=1)
endif()

set(targetname QGpgme)
if (${QT_MAJOR_VERSION} EQUAL "6")
    get_property(QtCore_MOC_EXECUTABLE TARGET Qt6::moc PROPERTY LOCATION)
    set(targetname "${targetname}Qt6")
endif()

add_library(${targetname} SHARED)

target_sources(${targetname} PRIVATE
    changeexpiryjob.cpp
    cleaner.cpp
    cryptoconfig.cpp
    dataprovider.cpp
    debug.cpp
    decryptverifyarchivejob.cpp
    decryptverifyjob.cpp
    defaultkeygenerationjob.cpp
    dn.cpp
    encryptarchivejob.cpp
    encryptjob.cpp
    filelistdataprovider.cpp
    importjob.cpp
    job.cpp
    listallkeysjob.cpp
    multideletejob.cpp
    qgpgme_debug.cpp
    qgpgmeaddexistingsubkeyjob.cpp
    qgpgmeadduseridjob.cpp
    qgpgmebackend.cpp
    qgpgmechangeexpiryjob.cpp
    qgpgmechangeownertrustjob.cpp
    qgpgmechangepasswdjob.cpp
    qgpgmedecryptjob.cpp
    qgpgmedecryptverifyarchivejob.cpp
    qgpgmedecryptverifyjob.cpp
    qgpgmedeletejob.cpp
    qgpgmedownloadjob.cpp
    qgpgmeencryptarchivejob.cpp
    qgpgmeencryptjob.cpp
    qgpgmeexportjob.cpp
    qgpgmegpgcardjob.cpp
    qgpgmeimportfromkeyserverjob.cpp
    qgpgmeimportjob.cpp
    qgpgmekeyformailboxjob.cpp
    qgpgmekeygenerationjob.cpp
    qgpgmekeylistjob.cpp
    qgpgmelistallkeysjob.cpp
    qgpgmenewcryptoconfig.cpp
    qgpgmequickjob.cpp
    qgpgmereceivekeysjob.cpp
    qgpgmerefreshsmimekeysjob.cpp
    qgpgmerevokekeyjob.cpp
    qgpgmesetprimaryuseridjob.cpp
    qgpgmesignarchivejob.cpp
    qgpgmesignencryptarchivejob.cpp
    qgpgmesignencryptjob.cpp
    qgpgmesignjob.cpp
    qgpgmesignkeyjob.cpp
    qgpgmetofupolicyjob.cpp
    qgpgmeverifydetachedjob.cpp
    qgpgmeverifyopaquejob.cpp
    qgpgmewkdlookupjob.cpp
    qgpgmewkdrefreshjob.cpp
    qgpgmewkspublishjob.cpp
    quickjob.cpp
    signarchivejob.cpp
    signencryptarchivejob.cpp
    signencryptjob.cpp
    signjob.cpp
    threadedjobmixin.cpp
    util.cpp
    verifydetachedjob.cpp
    verifyopaquejob.cpp
    wkdlookupresult.cpp
    wkdrefreshjob.cpp
)

set(qgpgme_PRIVATE_HEADERS
    changeexpiryjob_p.h
    cleaner.h
    decryptverifyarchivejob_p.h
    decryptverifyjob_p.h
    encryptarchivejob_p.h
    encryptjob_p.h
    importjob_p.h
    job_p.h
    listallkeysjob_p.h
    protocol_p.h
    qgpgme_export.h
    qgpgmeaddexistingsubkeyjob.h
    qgpgmeadduseridjob.h
    qgpgmebackend.h
    qgpgmechangeexpiryjob.h
    qgpgmechangeownertrustjob.h
    qgpgmechangepasswdjob.h
    qgpgmedecryptjob.h
    qgpgmedecryptverifyarchivejob.h
    qgpgmedecryptverifyjob.h
    qgpgmedeletejob.h
    qgpgmedownloadjob.h
    qgpgmeencryptarchivejob.h
    qgpgmeencryptjob.h
    qgpgmeexportjob.h
    qgpgmegpgcardjob.h
    qgpgmeimportfromkeyserverjob.h
    qgpgmeimportjob.h
    qgpgmekeyformailboxjob.h
    qgpgmekeygenerationjob.h
    qgpgmekeylistjob.h
    qgpgmelistallkeysjob.h
    qgpgmequickjob.h
    qgpgmereceivekeysjob.h
    qgpgmerefreshsmimekeysjob.h
    qgpgmerevokekeyjob.h
    qgpgmesetprimaryuseridjob.h
    qgpgmesignarchivejob.h
    qgpgmesignencryptarchivejob.h
    qgpgmesignencryptjob.h
    qgpgmesignjob.h
    qgpgmesignkeyjob.h
    qgpgmetofupolicyjob.h
    qgpgmeverifydetachedjob.h
    qgpgmeverifyopaquejob.h
    qgpgmewkdlookupjob.h
    qgpgmewkdrefreshjob.h
    qgpgmewkspublishjob.h
    quickjob_p.h
    signarchivejob_p.h
    signencryptarchivejob_p.h
    signencryptjob_p.h
    signjob_p.h
    threadedjobmixin.h
    util.h
    verifydetachedjob_p.h
    verifyopaquejob_p.h
    wkdrefreshjob_p.h
)

# the public headers
set(qgpgme_CAMELCASE_HEADERS
    AbstractImportJob
    AddExistingSubkeyJob
    AddUserIDJob
    ChangeExpiryJob
    ChangeOwnerTrustJob
    ChangePasswdJob
    CryptoConfig
    DN
    DataProvider
    Debug
    DecryptJob
    DecryptVerifyArchiveJob
    DecryptVerifyJob
    DefaultKeyGenerationJob
    DeleteJob
    DownloadJob
    EncryptArchiveJob
    EncryptJob
    ExportJob
    FileListDataProvider
    GpgCardJob
    ImportFromKeyserverJob
    ImportJob
    Job
    KeyForMailboxJob
    KeyGenerationJob
    KeyListJob
    ListAllKeysJob
    MultiDeleteJob
    Protocol
    QGpgMENewCryptoConfig
    QuickJob
    ReceiveKeysJob
    RefreshKeysJob
    RevokeKeyJob
    SetPrimaryUserIDJob
    SignArchiveJob
    SignEncryptArchiveJob
    SignEncryptJob
    SignJob
    SignKeyJob
    SpecialJob
    TofuPolicyJob
    VerifyDetachedJob
    VerifyOpaqueJob
    WKDLookupJob
    WKDLookupResult
    WKDRefreshJob
    WKSPublishJob
)

set(qgpgme_HEADERS)
foreach(header ${qgpgme_CAMELCASE_HEADERS})
    string(TOLOWER ${header} header_lc)
    file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/QGpgME/${header} "#include \"qgpgme/${header_lc}.h\"\n")
    list(APPEND qgpgme_HEADERS ${header_lc}.h)
endforeach()

set(qgpgme_MOC)
foreach(header ${qgpgme_HEADERS} ${qgpgme_PRIVATE_HEADERS})
    get_filename_component(absolute_path ${header} ABSOLUTE)
    get_filename_component(file_name ${header} NAME_WLE)

    if (${QT_MAJOR_VERSION} EQUAL "6")
        add_custom_command(
            OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${file_name}.moc
            COMMAND ${QtCore_MOC_EXECUTABLE} ${absolute_path} -o ${CMAKE_CURRENT_BINARY_DIR}/${file_name}.moc
        )
    else()
        add_custom_command(
            OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${file_name}.moc
            COMMAND ${QT_MOC_EXECUTABLE} ${absolute_path} -o ${CMAKE_CURRENT_BINARY_DIR}/${file_name}.moc
        )
    endif()

    list(APPEND qgpgme_MOC "${CMAKE_CURRENT_BINARY_DIR}/${file_name}.moc")
endforeach()
target_sources(${targetname} PRIVATE ${qgpgme_MOC})

target_link_libraries(${targetname} PUBLIC Gpgmepp Gpgme::Gpgme LibGpgError::LibGpgError Qt${QT_MAJOR_VERSION}::Core)

string(TOLOWER targetname targetname_lowercase)
set_target_properties(${targetname} PROPERTIES
    OUTPUT_NAME "${targetname_lowercase}"
    VERSION "${LIBQGPGME_SOVERSION}.${LIBQGPGME_LT_AGE}.${LIBQGPGME_LT_REVISION}"
    SOVERSION "${LIBQGPGME_SOVERSION}"
)

set(resolved_includedir "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_INCLUDEDIR}/qgpgme-qt${QT_MAJOR_VERSION}")
set(resolved_libdir "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}")
set(resolved_bindir "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_BINDIR}")
set(libsuffix "${CMAKE_SHARED_LIBRARY_SUFFIX}")

if (${QT_MAJOR_VERSION} EQUAL 6)
    set(config_suffix Qt6)
endif()

if (MSVC)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/QGpgme${config_suffix}Config-msvc.cmake.in.in
                   ${CMAKE_CURRENT_BINARY_DIR}/QGpgme${config_suffix}Config.cmake @ONLY)
elseif (WIN32)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/QGpgme${config_suffix}Config-w32.cmake.in.in
                   ${CMAKE_CURRENT_BINARY_DIR}/QGpgme${config_suffix}Config.cmake @ONLY)
else()
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/QGpgme${config_suffix}Config.cmake.in.in
                   ${CMAKE_CURRENT_BINARY_DIR}/QGpgme${config_suffix}Config.cmake @ONLY)
endif()
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/QGpgme${config_suffix}ConfigVersion.cmake.in
               ${CMAKE_CURRENT_BINARY_DIR}/QGpgme${config_suffix}ConfigVersion.cmake @ONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/qgpgme_version.h.in
               ${CMAKE_CURRENT_BINARY_DIR}/qgpgme_version.h)

if (MSVC)
    install(TARGETS ${targetname} DESTINATION ${resolved_bindir})
else()
    install(TARGETS ${targetname})
endif()

install(FILES ${qgpgme_HEADERS}
              ${CMAKE_CURRENT_BINARY_DIR}/qgpgme_version.h
              ${CMAKE_CURRENT_SOURCE_DIR}/qgpgme_export.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/qgpgme-qt${QT_MAJOR_VERSION}/qgpgme)
install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/QGpgME
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/qgpgme-qt${QT_MAJOR_VERSION})

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/QGpgme${config_suffix}ConfigVersion.cmake
              ${CMAKE_CURRENT_BINARY_DIR}/QGpgme${config_suffix}Config.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/QGpgme${config_suffix})
