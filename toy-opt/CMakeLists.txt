get_property(dialect_libs GLOBAL PROPERTY MLIR_DIALECT_LIBS)
get_property(conversion_libs GLOBAL PROPERTY MLIR_CONVERSION_LIBS)
set(LIBS
	${dialect_libs}
	${conversion_libs}
	MLIROptLib
	ToyOps
	HelloOps
	ToyToHello
	)
add_executable(toy-opt 
	toy-opt.cpp
	)
add_dependencies(toy-opt 
	ToyOpsInc
	HelloOpsInc
	)
add_dependencies(toy-opt 
	ToyOps
	HelloOps
	ToyToHello
	)
target_include_directories(toy-opt
	PRIVATE
	${PROJECT_SOURCE_DIR}
	${PROJECT_SOURCE_DIR}/include
	${PROJECT_BINARY_DIR}
	${PROJECT_BINARY_DIR}/include
	)
llvm_update_compile_flags(toy-opt)
target_link_libraries(toy-opt 
	PRIVATE 
	MLIRIR
	${LIBS} 
	${HelloLIBS}
	)

mlir_check_all_link_libraries(toy-opt)
