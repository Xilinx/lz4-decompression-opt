# Lz4 decompression optimization
This release contains HLS source files for a performance-optimzed version of LZ4 decompression. The IP is based on modified files from the Vitis Data Compression Library, but it is not part of the Vitis Data Compression Library

## Running HLS (including CSIM, CSYN,COSIM and POST-IMPL) 

See Build Instructions Below

## How to check the result of HLS CSIM and HLS COSIM results 

cat vitis_hls.log |grep -E '<INFO|PASS'

<INFO_COSIM_64b> set OUT_BYTES_VAL 8
<INFO_CSIM_64b> CSIM argv: ../../../../sample.lz4 ../../../../sample.out ../../../../sample.txt 
<INFO> length of comprssed file (byte?): 558
<INFO> inaxistream i: 0  0x1ba74064184d2204
<INFO> inaxistream i: 8  0x0a2a2f1bf1000002
<INFO> inaxistream i: 16  0x4320296328202a20
<INFO> inaxistream i: 24  0x746867697279706f
<INFO> inaxistream i: 32  0x6958203931303220
<INFO> inaxistream i: 40  0x6e49202c786e696c
<INFO> inaxistream i: 48  0x1c206c6c41202e63
<INFO> inaxistream i: 56  0x657365722073d100
<INFO> inaxistream i: 64  0x3b200a2e64657672
<INFO> outaxistreamsize (in bytes) : 1248
<INFO> outaxistream: 0x6328202a200a2a2f  bytes_remaining 1240  tlast 0
<INFO> outaxistream: 0x697279706f432029  bytes_remaining 1232  tlast 0
<INFO> outaxistream: 0x3931303220746867  bytes_remaining 1224  tlast 0
<INFO> outaxistream: 0x2c786e696c695820  bytes_remaining 1216  tlast 0
<INFO> outaxistream: 0x6c41202e636e4920  bytes_remaining 1208  tlast 0
<INFO> outaxistream: 0x737468676972206c  bytes_remaining 1200  tlast 0
<INFO> outaxistream: 0x6576726573657220  bytes_remaining 1192  tlast 0
<INFO> outaxistream: 0x2a200a2a200a2e64  bytes_remaining 1184  tlast 0
<INFO> outaxistream: 0x65736e6563694c20  bytes_remaining 1176  tlast 0
<INFO> TEST PASSED
<INFO_COSIM_64b> COSIM argv: ../../../../sample.lz4 ../../../../sample.out ../../../../sample.txt
<INFO> length of comprssed file (byte?): 558
<INFO> inaxistream i: 0  0x1ba74064184d2204
<INFO> inaxistream i: 8  0x0a2a2f1bf1000002
<INFO> inaxistream i: 16  0x4320296328202a20
<INFO> inaxistream i: 24  0x746867697279706f
<INFO> inaxistream i: 32  0x6958203931303220
<INFO> inaxistream i: 40  0x6e49202c786e696c
<INFO> inaxistream i: 48  0x1c206c6c41202e63
<INFO> inaxistream i: 56  0x657365722073d100
<INFO> inaxistream i: 64  0x3b200a2e64657672
<INFO> outaxistreamsize (in bytes) : 1248
<INFO> outaxistream: 0x6328202a200a2a2f  bytes_remaining 1240  tlast 0
<INFO> outaxistream: 0x697279706f432029  bytes_remaining 1232  tlast 0
<INFO> outaxistream: 0x3931303220746867  bytes_remaining 1224  tlast 0
<INFO> outaxistream: 0x2c786e696c695820  bytes_remaining 1216  tlast 0
<INFO> outaxistream: 0x6c41202e636e4920  bytes_remaining 1208  tlast 0
<INFO> outaxistream: 0x737468676972206c  bytes_remaining 1200  tlast 0
<INFO> outaxistream: 0x6576726573657220  bytes_remaining 1192  tlast 0
<INFO> outaxistream: 0x2a200a2a200a2e64  bytes_remaining 1184  tlast 0
<INFO> outaxistream: 0x65736e6563694c20  bytes_remaining 1176  tlast 0
<INFO> TEST PASSED
<INFO> length of comprssed file (byte?): 558
<INFO> inaxistream i: 0  0x1ba74064184d2204
<INFO> inaxistream i: 8  0x0a2a2f1bf1000002
<INFO> inaxistream i: 16  0x4320296328202a20
<INFO> inaxistream i: 24  0x746867697279706f
<INFO> inaxistream i: 32  0x6958203931303220
<INFO> inaxistream i: 40  0x6e49202c786e696c
<INFO> inaxistream i: 48  0x1c206c6c41202e63
<INFO> inaxistream i: 56  0x657365722073d100
<INFO> inaxistream i: 64  0x3b200a2e64657672
<INFO> outaxistreamsize (in bytes) : 1248
<INFO> outaxistream: 0x6328202a200a2a2f  bytes_remaining 1240  tlast 0
<INFO> outaxistream: 0x697279706f432029  bytes_remaining 1232  tlast 0
<INFO> outaxistream: 0x3931303220746867  bytes_remaining 1224  tlast 0
<INFO> outaxistream: 0x2c786e696c695820  bytes_remaining 1216  tlast 0
<INFO> outaxistream: 0x6c41202e636e4920  bytes_remaining 1208  tlast 0
<INFO> outaxistream: 0x737468676972206c  bytes_remaining 1200  tlast 0
<INFO> outaxistream: 0x6576726573657220  bytes_remaining 1192  tlast 0
<INFO> outaxistream: 0x2a200a2a200a2e64  bytes_remaining 1184  tlast 0
<INFO> outaxistream: 0x65736e6563694c20  bytes_remaining 1176  tlast 0
<INFO> TEST PASSED
INFO: [COSIM 212-1000] *** C/RTL co-simulation finished: PASS ***
<INFO> =============== HLS COSIM completed =============== 

############################################################################################################
############################################################################################################
# IP Build Instructions: compile HLS source files for optimized LZ4 Decompression

# create <workarea> directory
mkdir <workarea>
cd <workarea>

# Vitis Library cloning
git clone --branch v2022.2_update1 https://github.com/Xilinx/Vitis_Libraries.git
# NOTE: After cloning, Vitis Library is in <workarea>/Vitis_Libraries

# HLS_IP setup
mkdir <workarea>/HLS_IP
# Download Lz4_optimization-v1.0.zip is from GitHub Xilinx/lz4-decompression-opt repository
# place Lz4_optimization-v1.0.zip in <workarea>/HLS_IP 
cd <workarea>/HLS_IP
unzip Lz4_optimization-v1.0.zip

# use scripts to copy in necessary files from Vitis Library
cd <workarea>/HLS_IP/Lz4_optimization-v1.0/cp_scripts
# execute scripts 
./cp_L1_inc.sh  
./cp_L2_inc.sh  
./cp_L2_src.sh  
./cp_security_L1_inc.sh 
./cp_test_data.sh 

#source vivado tools 2023.2 tools setup
<vivado 2023.2 setup script>

# compile HLS IP
cd <workarea>/HLS_IP/Lz4_optimization-v1.0
vitis_hls -f run_hls_64b.tcl

# check for presence of IP file output_64b.zip in <workarea>/HLS_IP/Lz4_optimization-v1.0




