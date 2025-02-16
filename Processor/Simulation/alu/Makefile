# Usage:
# make sim TEST_TARGET=SIMULATE_ADD
# or
# make sim TEST_TARGET=SIMULATE_SUB
TEST_TARGET=SIMULATE_ADD	# Default

TEST_BENCH = alu_tb

# The order listing of the files is important
# Note: We don't include add_op.v or sub_op.v because they
# are controlled by Preprocessor constructs.
SUB_MODULES_FILES = ../../Modules/alu.v

MODULES_FILES = ${TEST_BENCH}.v ${SUB_MODULES_FILES}

ICESTORM_TOOLCHAIN = /usr/local
SIM_TOOLCHAIN = ${HOME}/.apio/packages/toolchain-iverilog

OUTPUT_PATH = /media/RAMDisk

.PHONY: all

sim: ${MODULES_FILES}
	@echo "##### Simulating via iverilog..."
	${SIM_TOOLCHAIN}/bin/iverilog -B "${SIM_TOOLCHAIN}/lib/ivl" -o ${OUTPUT_PATH}/netlist.out \
	-D$(TEST_TARGET) \
	-DNO_ICE40_DEFAULT_ASSIGNMENTS \
	${ICESTORM_TOOLCHAIN}/share/yosys/ice40/cells_sim.v ${MODULES_FILES}
	${SIM_TOOLCHAIN}/bin/vvp -M "${SIM_TOOLCHAIN}/lib/ivl" ${OUTPUT_PATH}/netlist.out
	gtkwave ${OUTPUT_PATH}/${TEST_BENCH}.vcd ${TEST_BENCH}.gtkw

# Notes:
# The macro NO_ICE40_DEFAULT_ASSIGNMENTS is used because we don't want
# any assignments applied to module IO parameters. If present the yosys toolchain
# fails with syntax errors.
# Early versions of cells_sim.v didn't have default assignment capabilities.
# It was added for SB_LUT4. See:
# https://webcache.googleusercontent.com/search?q=cache:hVxvTUjNeJgJ:https://git.magnatox.com/archive/yosys/commit/8aee80040de0b0812f2aec7ba4059c14407a0567+&cd=2&hl=en&ct=clnk&gl=us