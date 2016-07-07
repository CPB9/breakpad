project(breakpad)

cmake_minimum_required(VERSION 2.8.12)

if(UNIX)
    add_definitions(-fPIC)
endif()

set(SRC_PATH ${CMAKE_CURRENT_SOURCE_DIR}/src)

set(COMMON_PATH ${SRC_PATH}/common)

set(BREAKPAD_COMMON_SRC
    ${COMMON_PATH}/basictypes.h
    ${COMMON_PATH}/byte_cursor.h
    ${COMMON_PATH}/convert_UTF.c
    ${COMMON_PATH}/convert_UTF.h
    ${COMMON_PATH}/language.cc
    ${COMMON_PATH}/language.h
    ${COMMON_PATH}/md5.cc
    ${COMMON_PATH}/md5.h
    ${COMMON_PATH}/memory.h
    ${COMMON_PATH}/memory_range.h
    ${COMMON_PATH}/module.cc
    ${COMMON_PATH}/module.h
    ${COMMON_PATH}/scoped_ptr.h
    ${COMMON_PATH}/simple_string_dictionary.cc
    ${COMMON_PATH}/simple_string_dictionary.h
    ${COMMON_PATH}/stabs_reader.cc
    ${COMMON_PATH}/stabs_reader.h
    ${COMMON_PATH}/stabs_to_module.cc
    ${COMMON_PATH}/stabs_to_module.h
    ${COMMON_PATH}/string_conversion.cc
    ${COMMON_PATH}/string_conversion.h
    ${COMMON_PATH}/symbol_data.h
    ${COMMON_PATH}/test_assembler.cc
    ${COMMON_PATH}/test_assembler.h
    ${COMMON_PATH}/unordered.h
    ${COMMON_PATH}/using_std_string.h
    ${COMMON_PATH}/dwarf/bytereader-inl.h
    ${COMMON_PATH}/dwarf/bytereader.cc
    ${COMMON_PATH}/dwarf/bytereader.h
    ${COMMON_PATH}/dwarf/cfi_assembler.cc
    ${COMMON_PATH}/dwarf/cfi_assembler.h
    ${COMMON_PATH}/dwarf/dwarf2diehandler.cc
    ${COMMON_PATH}/dwarf/dwarf2diehandler.h
    ${COMMON_PATH}/dwarf/dwarf2enums.h
    ${COMMON_PATH}/dwarf/dwarf2reader.cc
    ${COMMON_PATH}/dwarf/dwarf2reader.h
    ${COMMON_PATH}/dwarf/dwarf2reader_test_common.h
    ${COMMON_PATH}/dwarf/elf_reader.cc
    ${COMMON_PATH}/dwarf/elf_reader.h
    ${COMMON_PATH}/dwarf/functioninfo.cc
    ${COMMON_PATH}/dwarf/functioninfo.h
    ${COMMON_PATH}/dwarf/line_state_machine.h
    ${COMMON_PATH}/dwarf/types.h
    ${COMMON_PATH}/dwarf_cfi_to_module.cc
    ${COMMON_PATH}/dwarf_cfi_to_module.h
    ${COMMON_PATH}/dwarf_cu_to_module.cc
    ${COMMON_PATH}/dwarf_cu_to_module.h
    ${COMMON_PATH}/dwarf_line_to_module.cc
    ${COMMON_PATH}/dwarf_line_to_module.h

)

# set(BREAKPAD_COMMON_ANDROID_SRC
#     ${COMMON_PATH}/android/breakpad_getcontext.S
#     ${COMMON_PATH}/android/include/elf.h
#     ${COMMON_PATH}/android/include/link.h
#     ${COMMON_PATH}/android/include/sgidefs.h
#     ${COMMON_PATH}/android/include/stab.h
#     ${COMMON_PATH}/android/include/sys/procfs.h
#     ${COMMON_PATH}/android/include/sys/signal.h
#     ${COMMON_PATH}/android/include/sys/user.h
#     ${COMMON_PATH}/android/include/ucontext.h
#     ${COMMON_PATH}/android/testing/include/wchar.h
#     ${COMMON_PATH}/android/testing/mkdtemp.h
#     ${COMMON_PATH}/android/testing/pthread_fixes.h
#     ${COMMON_PATH}/android/ucontext_constants.h
# )

set(BREAKPAD_COMMON_LINUX_SRC
    ${COMMON_PATH}/linux/crc32.cc
    ${COMMON_PATH}/linux/crc32.h
    ${COMMON_PATH}/linux/dump_symbols.cc
    ${COMMON_PATH}/linux/dump_symbols.h
    ${COMMON_PATH}/linux/eintr_wrapper.h
    ${COMMON_PATH}/linux/elf_core_dump.cc
    ${COMMON_PATH}/linux/elf_core_dump.h
    ${COMMON_PATH}/linux/elf_gnu_compat.h
    ${COMMON_PATH}/linux/elf_symbols_to_module.cc
    ${COMMON_PATH}/linux/elf_symbols_to_module.h
    ${COMMON_PATH}/linux/elfutils-inl.h
    ${COMMON_PATH}/linux/elfutils.cc
    ${COMMON_PATH}/linux/elfutils.h
    ${COMMON_PATH}/linux/file_id.cc
    ${COMMON_PATH}/linux/file_id.h
    ${COMMON_PATH}/linux/google_crashdump_uploader.cc
    ${COMMON_PATH}/linux/google_crashdump_uploader.h
    ${COMMON_PATH}/linux/guid_creator.cc
    ${COMMON_PATH}/linux/guid_creator.h
    ${COMMON_PATH}/linux/http_upload.cc
    ${COMMON_PATH}/linux/http_upload.h
    ${COMMON_PATH}/linux/ignore_ret.h
    ${COMMON_PATH}/linux/libcurl_wrapper.cc
    ${COMMON_PATH}/linux/libcurl_wrapper.h
    ${COMMON_PATH}/linux/linux_libc_support.cc
    ${COMMON_PATH}/linux/linux_libc_support.h
    ${COMMON_PATH}/linux/memory_mapped_file.cc
    ${COMMON_PATH}/linux/memory_mapped_file.h
    ${COMMON_PATH}/linux/safe_readlink.cc
    ${COMMON_PATH}/linux/safe_readlink.h
    ${COMMON_PATH}/linux/synth_elf.cc
    ${COMMON_PATH}/linux/synth_elf.h
)

# set(BREAKPAD_COMMON_MAC_SRC
#     ${COMMON_PATH}/mac/arch_utilities.cc
#     ${COMMON_PATH}/mac/arch_utilities.h
#     ${COMMON_PATH}/mac/bootstrap_compat.cc
#     ${COMMON_PATH}/mac/bootstrap_compat.h
#     ${COMMON_PATH}/mac/byteswap.h
#     ${COMMON_PATH}/mac/dump_syms.h
#     ${COMMON_PATH}/mac/dump_syms.cc
#     ${COMMON_PATH}/mac/file_id.cc
#     ${COMMON_PATH}/mac/file_id.h
#     ${COMMON_PATH}/mac/GTMDefines.h
#     ${COMMON_PATH}/mac/GTMLogger.h
#     ${COMMON_PATH}/mac/GTMLogger.m
#     ${COMMON_PATH}/mac/HTTPMultipartUpload.h
#     ${COMMON_PATH}/mac/HTTPMultipartUpload.m
#     ${COMMON_PATH}/mac/MachIPC.h
#     ${COMMON_PATH}/mac/MachIPC.mm
#     ${COMMON_PATH}/mac/macho_id.cc
#     ${COMMON_PATH}/mac/macho_id.h
#     ${COMMON_PATH}/mac/macho_reader.cc
#     ${COMMON_PATH}/mac/macho_reader.h
#     ${COMMON_PATH}/mac/macho_utilities.cc
#     ${COMMON_PATH}/mac/macho_utilities.h
#     ${COMMON_PATH}/mac/macho_walker.cc
#     ${COMMON_PATH}/mac/macho_walker.h
#     ${COMMON_PATH}/mac/scoped_task_suspend-inl.h
#     ${COMMON_PATH}/mac/string_utilities.cc
#     ${COMMON_PATH}/mac/string_utilities.h
#     ${COMMON_PATH}/mac/super_fat_arch.h
# )

# set(BREAKPAD_COMMON_SOLARIS_SRC
#     ${COMMON_PATH}/solaris/dump_symbols.cc
#     ${COMMON_PATH}/solaris/dump_symbols.h
#     ${COMMON_PATH}/solaris/file_id.cc
#     ${COMMON_PATH}/solaris/file_id.h
#     ${COMMON_PATH}/solaris/guid_creator.cc
#     ${COMMON_PATH}/solaris/guid_creator.h
#     ${COMMON_PATH}/solaris/message_output.h
# )

set(BREAKPAD_COMMON_WINDOWS_SRC
    ${COMMON_PATH}/windows/dia_util.cc
    ${COMMON_PATH}/windows/dia_util.h
    ${COMMON_PATH}/windows/guid_string.cc
    ${COMMON_PATH}/windows/guid_string.h
    ${COMMON_PATH}/windows/http_upload.cc
    ${COMMON_PATH}/windows/http_upload.h
    ${COMMON_PATH}/windows/omap.cc
    ${COMMON_PATH}/windows/omap.h
    ${COMMON_PATH}/windows/omap_internal.h
    ${COMMON_PATH}/windows/pdb_source_line_writer.cc
    ${COMMON_PATH}/windows/pdb_source_line_writer.h
    ${COMMON_PATH}/windows/string_utils-inl.h
    ${COMMON_PATH}/windows/string_utils.cc
)

if(UNIX)
    add_library(breakpad-common
        ${BREAKPAD_COMMON_SRC}
        ${BREAKPAD_COMMON_LINUX_SRC}
    )
    target_compile_options(breakpad-common PUBLIC -DHAVE_A_OUT_H)
# elseif(APPLE)
#     add_library(breakpad-common
#         ${BREAKPAD_COMMON_SRC}
#         ${BREAKPAD_COMMON_MAC_SRC}
#     )
#     target_compile_options(breakpad-common PUBLIC -DHAVE_MACH_O_NLIST_H)
elseif(WIN32)
    add_library(breakpad-common
        ${BREAKPAD_COMMON_SRC}
        ${BREAKPAD_COMMON_WINDOWS_SRC}
    )
endif()

target_include_directories(breakpad-common PUBLIC ${SRC_PATH})

set(LIBDISASM_PATH ${SRC_PATH}/third_party/libdisasm)

set(LIBDISASM_SRC
    ${LIBDISASM_PATH}/ia32_implicit.c
    ${LIBDISASM_PATH}/ia32_implicit.h
    ${LIBDISASM_PATH}/ia32_insn.c
    ${LIBDISASM_PATH}/ia32_insn.h
    ${LIBDISASM_PATH}/ia32_invariant.c
    ${LIBDISASM_PATH}/ia32_invariant.h
    ${LIBDISASM_PATH}/ia32_modrm.c
    ${LIBDISASM_PATH}/ia32_modrm.h
    ${LIBDISASM_PATH}/ia32_opcode_tables.c
    ${LIBDISASM_PATH}/ia32_opcode_tables.h
    ${LIBDISASM_PATH}/ia32_operand.c
    ${LIBDISASM_PATH}/ia32_operand.h
    ${LIBDISASM_PATH}/ia32_reg.c
    ${LIBDISASM_PATH}/ia32_reg.h
    ${LIBDISASM_PATH}/ia32_settings.c
    ${LIBDISASM_PATH}/ia32_settings.h
    ${LIBDISASM_PATH}/libdis.h
    ${LIBDISASM_PATH}/qword.h
    ${LIBDISASM_PATH}/x86_disasm.c
    ${LIBDISASM_PATH}/x86_format.c
    ${LIBDISASM_PATH}/x86_imm.c
    ${LIBDISASM_PATH}/x86_imm.h
    ${LIBDISASM_PATH}/x86_insn.c
    ${LIBDISASM_PATH}/x86_misc.c
    ${LIBDISASM_PATH}/x86_operand_list.c
    ${LIBDISASM_PATH}/x86_operand_list.h
)

add_library(disasm ${LIBDISASM_SRC})
target_include_directories(disasm PUBLIC ${LIBDISASM_PATH})

set(PROCESSOR_PATH ${SRC_PATH}/processor)

set(BREAKPAD_PROCESSOR_SRC
    ${PROCESSOR_PATH}/address_map-inl.h
    ${PROCESSOR_PATH}/address_map.h
    ${PROCESSOR_PATH}/basic_code_module.h
    ${PROCESSOR_PATH}/basic_code_modules.cc
    ${PROCESSOR_PATH}/basic_code_modules.h
    ${PROCESSOR_PATH}/basic_source_line_resolver.cc
    ${PROCESSOR_PATH}/basic_source_line_resolver_types.h
    ${PROCESSOR_PATH}/call_stack.cc
    ${PROCESSOR_PATH}/cfi_frame_info-inl.h
    ${PROCESSOR_PATH}/cfi_frame_info.cc
    ${PROCESSOR_PATH}/cfi_frame_info.h
    ${PROCESSOR_PATH}/contained_range_map-inl.h
    ${PROCESSOR_PATH}/contained_range_map.h
    ${PROCESSOR_PATH}/disassembler_x86.cc
    ${PROCESSOR_PATH}/disassembler_x86.h
    ${PROCESSOR_PATH}/dump_context.cc
    ${PROCESSOR_PATH}/dump_object.cc
    ${PROCESSOR_PATH}/exploitability.cc
    ${PROCESSOR_PATH}/exploitability_linux.cc
    ${PROCESSOR_PATH}/exploitability_linux.h
    ${PROCESSOR_PATH}/exploitability_win.cc
    ${PROCESSOR_PATH}/exploitability_win.h
    ${PROCESSOR_PATH}/fast_source_line_resolver.cc
    ${PROCESSOR_PATH}/fast_source_line_resolver_types.h
    ${PROCESSOR_PATH}/linked_ptr.h
    ${PROCESSOR_PATH}/logging.cc
    ${PROCESSOR_PATH}/logging.h
    ${PROCESSOR_PATH}/map_serializers-inl.h
    ${PROCESSOR_PATH}/map_serializers.h
    ${PROCESSOR_PATH}/microdump_processor.cc
    ${PROCESSOR_PATH}/minidump.cc
    ${PROCESSOR_PATH}/minidump_processor.cc
    ${PROCESSOR_PATH}/module_comparer.cc
    ${PROCESSOR_PATH}/module_comparer.h
    ${PROCESSOR_PATH}/module_factory.h
    ${PROCESSOR_PATH}/module_serializer.cc
    ${PROCESSOR_PATH}/module_serializer.h
    ${PROCESSOR_PATH}/pathname_stripper.cc
    ${PROCESSOR_PATH}/pathname_stripper.h
    ${PROCESSOR_PATH}/postfix_evaluator-inl.h
    ${PROCESSOR_PATH}/postfix_evaluator.h
    ${PROCESSOR_PATH}/proc_maps_linux.cc
    ${PROCESSOR_PATH}/process_state.cc
    ${PROCESSOR_PATH}/range_map-inl.h
    ${PROCESSOR_PATH}/range_map.h
    ${PROCESSOR_PATH}/simple_serializer-inl.h
    ${PROCESSOR_PATH}/simple_serializer.h
    ${PROCESSOR_PATH}/simple_symbol_supplier.cc
    ${PROCESSOR_PATH}/simple_symbol_supplier.h
    ${PROCESSOR_PATH}/source_line_resolver_base.cc
    ${PROCESSOR_PATH}/source_line_resolver_base_types.h
    ${PROCESSOR_PATH}/stack_frame_cpu.cc
    ${PROCESSOR_PATH}/stack_frame_symbolizer.cc
    ${PROCESSOR_PATH}/stackwalk_common.cc
    ${PROCESSOR_PATH}/stackwalk_common.h
    ${PROCESSOR_PATH}/stackwalker.cc
    ${PROCESSOR_PATH}/stackwalker_address_list.cc
    ${PROCESSOR_PATH}/stackwalker_address_list.h
    ${PROCESSOR_PATH}/stackwalker_amd64.cc
    ${PROCESSOR_PATH}/stackwalker_amd64.h
    ${PROCESSOR_PATH}/stackwalker_arm.cc
    ${PROCESSOR_PATH}/stackwalker_arm.h
    ${PROCESSOR_PATH}/stackwalker_arm64.cc
    ${PROCESSOR_PATH}/stackwalker_arm64.h
    ${PROCESSOR_PATH}/stackwalker_mips.cc
    ${PROCESSOR_PATH}/stackwalker_mips.h
    ${PROCESSOR_PATH}/stackwalker_ppc.cc
    ${PROCESSOR_PATH}/stackwalker_ppc.h
    ${PROCESSOR_PATH}/stackwalker_ppc64.cc
    ${PROCESSOR_PATH}/stackwalker_ppc64.h
    ${PROCESSOR_PATH}/stackwalker_selftest.cc
    ${PROCESSOR_PATH}/stackwalker_sparc.cc
    ${PROCESSOR_PATH}/stackwalker_sparc.h
    ${PROCESSOR_PATH}/stackwalker_x86.cc
    ${PROCESSOR_PATH}/stackwalker_x86.h
    ${PROCESSOR_PATH}/static_address_map-inl.h
    ${PROCESSOR_PATH}/static_address_map.h
    ${PROCESSOR_PATH}/static_contained_range_map-inl.h
    ${PROCESSOR_PATH}/static_contained_range_map.h
    ${PROCESSOR_PATH}/static_map-inl.h
    ${PROCESSOR_PATH}/static_map.h
    ${PROCESSOR_PATH}/static_map_iterator-inl.h
    ${PROCESSOR_PATH}/static_map_iterator.h
    ${PROCESSOR_PATH}/static_range_map-inl.h
    ${PROCESSOR_PATH}/static_range_map.h
    ${PROCESSOR_PATH}/symbolic_constants_win.cc
    ${PROCESSOR_PATH}/symbolic_constants_win.h
    ${PROCESSOR_PATH}/synth_minidump.cc
    ${PROCESSOR_PATH}/synth_minidump.h
    ${PROCESSOR_PATH}/tokenize.cc
    ${PROCESSOR_PATH}/tokenize.h
    ${PROCESSOR_PATH}/windows_frame_info.h
)

add_library(breakpad-processor
    ${BREAKPAD_PROCESSOR_SRC}
)

target_include_directories(breakpad-processor PUBLIC ${SRC_PATH})
target_link_libraries(breakpad-processor breakpad-common disasm)

add_executable(minidump_dump ${PROCESSOR_PATH}/minidump_dump.cc)
target_link_libraries(minidump_dump breakpad-processor)

add_executable(minidump_stackwalk ${PROCESSOR_PATH}/minidump_stackwalk.cc)
target_link_libraries(minidump_stackwalk breakpad-processor)

set(CLIENT_PATH ${SRC_PATH}/client)

if(WIN32)
    add_library(breakpad_client
        ${CLIENT_PATH}/windows/common/auto_critical_section.h
        ${CLIENT_PATH}/windows/common/ipc_protocol.h
        ${CLIENT_PATH}/windows/crash_generation/client_info.cc
        ${CLIENT_PATH}/windows/crash_generation/client_info.h
        ${CLIENT_PATH}/windows/crash_generation/crash_generation_client.cc
        ${CLIENT_PATH}/windows/crash_generation/crash_generation_client.h
        ${CLIENT_PATH}/windows/crash_generation/crash_generation_server.cc
        ${CLIENT_PATH}/windows/crash_generation/crash_generation_server.h
        ${CLIENT_PATH}/windows/crash_generation/minidump_generator.cc
        ${CLIENT_PATH}/windows/crash_generation/minidump_generator.h
        ${CLIENT_PATH}/windows/handler/exception_handler.cc
        ${CLIENT_PATH}/windows/handler/exception_handler.h
        ${CLIENT_PATH}/windows/sender/crash_report_sender.cc
        ${CLIENT_PATH}/windows/sender/crash_report_sender.h
    )

    add_executable(dump_syms ${SRC_PATH}/tools/windows/dump_syms/dump_syms.cc)
    target_link_libraries(dump_syms breakpad-common)
else()
    add_library(breakpad-client
        ${CLIENT_PATH}/linux/crash_generation/client_info.h
        ${CLIENT_PATH}/linux/crash_generation/crash_generation_client.cc
        ${CLIENT_PATH}/linux/crash_generation/crash_generation_client.h
        ${CLIENT_PATH}/linux/crash_generation/crash_generation_server.cc
        ${CLIENT_PATH}/linux/crash_generation/crash_generation_server.h
        ${CLIENT_PATH}/linux/dump_writer_common/mapping_info.h
        ${CLIENT_PATH}/linux/dump_writer_common/raw_context_cpu.h
        ${CLIENT_PATH}/linux/dump_writer_common/thread_info.cc
        ${CLIENT_PATH}/linux/dump_writer_common/thread_info.h
        ${CLIENT_PATH}/linux/dump_writer_common/ucontext_reader.cc
        ${CLIENT_PATH}/linux/dump_writer_common/ucontext_reader.h
        ${CLIENT_PATH}/linux/handler/exception_handler.cc
        ${CLIENT_PATH}/linux/handler/exception_handler.h
        ${CLIENT_PATH}/linux/handler/microdump_extra_info.h
        ${CLIENT_PATH}/linux/handler/minidump_descriptor.cc
        ${CLIENT_PATH}/linux/handler/minidump_descriptor.h
        ${CLIENT_PATH}/linux/log/log.cc
        ${CLIENT_PATH}/linux/log/log.h
        ${CLIENT_PATH}/linux/microdump_writer/microdump_writer.cc
        ${CLIENT_PATH}/linux/microdump_writer/microdump_writer.h
        ${CLIENT_PATH}/linux/minidump_writer/cpu_set.h
        ${CLIENT_PATH}/linux/minidump_writer/directory_reader.h
        ${CLIENT_PATH}/linux/minidump_writer/line_reader.h
        ${CLIENT_PATH}/linux/minidump_writer/linux_core_dumper.cc
        ${CLIENT_PATH}/linux/minidump_writer/linux_core_dumper.h
        ${CLIENT_PATH}/linux/minidump_writer/linux_dumper.cc
        ${CLIENT_PATH}/linux/minidump_writer/linux_dumper.h
        ${CLIENT_PATH}/linux/minidump_writer/linux_ptrace_dumper.cc
        ${CLIENT_PATH}/linux/minidump_writer/linux_ptrace_dumper.h
        ${CLIENT_PATH}/linux/minidump_writer/minidump_writer.cc
        ${CLIENT_PATH}/linux/minidump_writer/minidump_writer.h
        ${CLIENT_PATH}/linux/minidump_writer/proc_cpuinfo_reader.h
        ${CLIENT_PATH}/minidump_file_writer.cc
        ${CLIENT_PATH}/minidump_file_writer.h
        ${CLIENT_PATH}/minidump_file_writer-inl.h
    )

    add_executable(dump_syms ${SRC_PATH}/tools/linux/dump_syms/dump_syms.cc)
    target_link_libraries(dump_syms breakpad-common)
endif()

target_link_libraries(breakpad-client breakpad-common)
