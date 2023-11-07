## References:
https://github.com/ChHanXiao/license-plate-recoginition

## step 1
`git clone https://github.com/ChHanXiao/license-plate-recoginition.git`

## step 2
install polygraphy: 

`pip install colored polygraphy --extra-index-url https://pypi.ngc.nvidia.com`

## step 3

run export_onnx.py

## step 4

convert onnx to trt engine

fp16: 

`trtexec --onnx=workspace/lpr_20231102_all_types.onnx --saveEngine=workspace/lpr_20231102_all_types_fp16.engine --fp16 --workspace=10240`
  
int8:
 - modify dataloader_for_calibration.py, use your dataset
 - `polygraphy convert ./workspace/lpr_20231102_all_types.onnx --int8 --data-loader-script ./dataloader_for_calibration.py --calibration-cache ./workspace/lpr_calib.cache -o ./workspace/lpr_20231102_all_types_int8.engine`
## step 5
run detect_lpr_trt.py
