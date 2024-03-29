project(umfpack)

cmake_minimum_required(VERSION 3.20)

set (SRC
	UMFPACK/Source/umf_multicompile.c 
	UMFPACK/Source/umfpack_global.c 
	UMFPACK/Source/umf_ltsolve.c 
	UMFPACK/Source/umf_utsolve.c 
	UMFPACK/Source/umf_triplet.c 
	UMFPACK/Source/umf_assemble.c 
	UMFPACK/Source/umf_store_lu.c 
	UMFPACK/Source/umfpack_solve.c 
	AMD/Source/amd_1.c 
	AMD/Source/amd_2.c 
	AMD/Source/amd_aat.c 
	AMD/Source/amd_control.c 
	AMD/Source/amd_defaults.c 
	AMD/Source/amd_global.c 
	AMD/Source/amd_dump.c 
	AMD/Source/amd_info.c 
	AMD/Source/amd_order.c 
	AMD/Source/amd_post_tree.c 
	AMD/Source/amd_postorder.c 
	AMD/Source/amd_preprocess.c 
	AMD/Source/amd_valid.c 
	UMFPACK/Source/umf_2by2.c 
	UMFPACK/Source/umf_analyze.c 
	UMFPACK/Source/umf_apply_order.c 
	UMFPACK/Source/umf_blas3_update.c 
	UMFPACK/Source/umf_build_tuples.c 
	UMFPACK/Source/umf_colamd.c 
	UMFPACK/Source/umf_create_element.c 
	UMFPACK/Source/umf_dump.c 
	UMFPACK/Source/umf_extend_front.c 
	UMFPACK/Source/umf_free.c 
	UMFPACK/Source/umf_fsize.c 
	UMFPACK/Source/umf_garbage_collection.c 
	UMFPACK/Source/umf_get_memory.c 
	UMFPACK/Source/umf_grow_front.c 
	UMFPACK/Source/umf_init_front.c 
	UMFPACK/Source/umf_is_permutation.c 
	UMFPACK/Source/umf_kernel.c 
	UMFPACK/Source/umf_kernel_init.c 
	UMFPACK/Source/umf_kernel_wrapup.c 
	UMFPACK/Source/umf_local_search.c 
	UMFPACK/Source/umf_lsolve.c 
	UMFPACK/Source/umf_malloc.c 
	UMFPACK/Source/umf_mem_alloc_element.c 
	UMFPACK/Source/umf_mem_alloc_head_block.c 
	UMFPACK/Source/umf_mem_alloc_tail_block.c 
	UMFPACK/Source/umf_mem_free_tail_block.c 
	UMFPACK/Source/umf_mem_init_memoryspace.c 
	UMFPACK/Source/umf_realloc.c 
	UMFPACK/Source/umf_report_perm.c 
	UMFPACK/Source/umf_report_vector.c 
	UMFPACK/Source/umf_row_search.c 
	UMFPACK/Source/umf_scale.c 
	UMFPACK/Source/umf_scale_column.c 
	UMFPACK/Source/umf_set_stats.c 
	UMFPACK/Source/umf_singletons.c 
	UMFPACK/Source/umf_solve.c 
	UMFPACK/Source/umf_start_front.c 
	UMFPACK/Source/umf_symbolic_usage.c 
	UMFPACK/Source/umf_transpose.c 
	UMFPACK/Source/umf_tuple_lengths.c 
	UMFPACK/Source/umf_usolve.c 
	UMFPACK/Source/umf_valid_numeric.c 
	UMFPACK/Source/umf_valid_symbolic.c 
	UMFPACK/Source/umfpack_col_to_triplet.c 
	UMFPACK/Source/umfpack_defaults.c 
	UMFPACK/Source/umfpack_free_numeric.c 
	UMFPACK/Source/umfpack_free_symbolic.c 
	UMFPACK/Source/umfpack_get_determinant.c 
	UMFPACK/Source/umfpack_get_lunz.c 
	UMFPACK/Source/umfpack_get_numeric.c 
	UMFPACK/Source/umfpack_get_symbolic.c 
	UMFPACK/Source/umfpack_load_numeric.c 
	UMFPACK/Source/umfpack_load_symbolic.c 
	UMFPACK/Source/umfpack_numeric.c 
	UMFPACK/Source/umfpack_qsymbolic.c 
	UMFPACK/Source/umfpack_report_control.c 
	UMFPACK/Source/umfpack_report_info.c 
	UMFPACK/Source/umfpack_report_matrix.c 
	UMFPACK/Source/umfpack_report_numeric.c 
	UMFPACK/Source/umfpack_report_perm.c 
	UMFPACK/Source/umfpack_report_status.c 
	UMFPACK/Source/umfpack_report_symbolic.c 
	UMFPACK/Source/umfpack_report_triplet.c 
	UMFPACK/Source/umfpack_report_vector.c 
	UMFPACK/Source/umfpack_save_numeric.c 
	UMFPACK/Source/umfpack_save_symbolic.c 
	UMFPACK/Source/umfpack_scale.c 
	UMFPACK/Source/umfpack_symbolic.c 
	UMFPACK/Source/umfpack_tictoc.c 
	UMFPACK/Source/umfpack_timer.c 
	UMFPACK/Source/umfpack_transpose.c 
	UMFPACK/Source/umfpack_triplet_to_col.c)

if (UMFPACK_SHARED)
add_library(umfpack SHARED ${SRC})
else ()
add_library(umfpack ${SRC})
endif ()
if (BLAS_FOUND)
target_compile_options(umfpack PRIVATE -DDINT)
target_link_directories(umfpack PUBLIC ${BLAS_STATIC_LIBRARY_DIRS})
target_link_libraries(umfpack PUBLIC ${BLAS_STATIC_LIBRARIES})
else ()
target_compile_options(umfpack PRIVATE -DDINT -DNBLAS)
endif ()
target_include_directories(umfpack PUBLIC
    AMD/Source 
    AMD/Include 
    UMFPACK/Source 
    UMFPACK/Include 
    UFconfig)

