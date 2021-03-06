#
# Copyright 2019 Xilinx, Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

ifndef MKLROOT
$(error [ERROR] MKLROOT not defined)
endif

CXX	= g++
CFLAGS	= -O2 -DMKL_ILP64 -m64 -fopenmp -static -std=c++11 -I${MKLROOT}/include
MKL_LIBS = -L$(MKLROOT)/lib/intel64 -Wl,--start-group -lmkl_intel_lp64 -lmkl_gnu_thread -lmkl_core -Wl,--end-group

all : sgemv

sgemv  : sgemv_mkl_bench sgemv_mkl_gen sgemv_mkl_gen_short

sgemv_mkl_bench  : gemv_mkl_bench.cpp
	$(CXX) $(CFLAGS) -DUSE_FLOAT_PRECISION -o $@ $^ $(MKL_LIBS) -lpthread -lm

dgemv_mkl_bench  : gemv_mkl_bench.cpp
	$(CXX) $(CFLAGS) -DUSE_DOUBLE_PRECISION -o $@ $^ $(MKL_LIBS) -lpthread -lm

sgemv_mkl_gen: gemv_mkl_gen_bin.cpp
	$(CXX) $(CFLAGS) -DUSE_FLOAT_PRECISION -o $@ $^ $(MKL_LIBS) -lpthread -lm

dgemv_mkl_gen: gemv_mkl_gen_bin.cpp
	$(CXX) $(CFLAGS) -DUSE_DOUBLE_PRECISION -o $@ $^ $(MKL_LIBS) -lpthread -lm

sgemv_mkl_gen_short: gemv_mkl_gen_bin.cpp
	$(CXX) $(CFLAGS) -DUSE_SHORT -o $@ $^ $(MKL_LIBS) -lpthread -lm

clean:
	rm -f log-*.txt perf_gemv_mkl_bench.csv *.o *~ sgemv_mkl_bench dgemv_mkl_bench sgemv_mkl_gen dgemv_mkl_gen sgemv_mkl_gen_short
