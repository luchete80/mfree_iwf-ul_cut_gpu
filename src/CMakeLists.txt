SET(BUILD_GPU ON)


project (mfree_iwf LANGUAGES CXX CUDA)

include_directories(${PROJECT_SOURCE_DIR})

include_directories(${GLM_INC_DIR})
include_directories(${THRUST_DIR})
# target_link_libraries (gpuweldform cuNSearch )

#set (CMAKE_CXX_FLAGS "-fopenmp")


set(CMAKE_CXX_STANDARD 11) #LIKE IN CUNSearch, this allows to include string (conflicts with CXX17)!!!
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# --fmad=true and --fmad=false enables and disables the contraction respectively. 
 # This switch is supported only when the --gpu-architecture option is set with     
 # compute_20, sm_20, or higher. For other architecture classes, the contraction is     
  # always enabled. 
 # The --use_fast_math option implies --fmad=true, and enables the contraction.
set(CMAKE_CUDA_FLAGS "${CMAKE_CUDA_FLAGS} --fmad=false --prec-sqrt=true --ftz=false --prec-div=true -DTHRUST_IGNORE_CUB_VERSION_CHECK")

FILE(GLOB SRCS *.h *.cu *.cpp)

ADD_EXECUTABLE(mfree_iwf ${SRCS})