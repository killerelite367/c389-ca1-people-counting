# Model and video evaluation

## Held-out image test

The improved notebook recorded these overall values on **38 test images with 80 labeled instances**. The checkpoint was trained with YOLO26n, 100 epochs, image size 640 and batch size 16 on dataset version 4.

| Model | Precision | Recall | mAP50 | mAP50–95 |
|---|---:|---:|---:|---:|
| Original model | Pending | Pending | Pending | Pending |
| Improved checkpoint | 0.864 | 0.889 | 0.937 | 0.608 |

The [per-class test metrics](improved-detector/baseline_metrics.json), [training results](improved-detector/results.csv), [precision–recall graph](improved-detector/BoxPR_curve.png) and [confusion matrix](improved-detector/confusion_matrix.png) come from the saved Drive run. Record the original checkpoint's results on the same split before drawing a before-and-after conclusion.

## Saved Gradio example

[T4 outputs and settings](t4-video-example/) come from test_video2.MOV, run 20261106T100129Z_fd1300d5. The example used the improved checkpoint, image size 640, confidence 0.10, ByteTrack with a 30-frame buffer and a one-second wait rule. The CSV reports **ID 1 at 3.70 s** and **ID 3 at 2.67 s**. These are system predictions. The saved ground-truth and ID-mapping CSVs are blank templates, so manual video accuracy is pending.

In the annotated output, a passing car covers the pedestrians on the left curb. The pedestrian in jeans appears as ID 3 while waiting and ID 73 after the car passes. Compare that case by hand to check whether a tracker change reconnects the wait and crossing correctly. Use a separate held-out clip for final accuracy measurements. The [saved video run](https://drive.google.com/drive/folders/1YHHlNx-iHKgIxCbuFNZG2WSH5OyswcO_) requires Drive access.
