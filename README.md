

# Mask DINO for MapChallenge Instance Segmentation

## Installation
See [installation instructions](INSTALL.md).

## Pretrained Model
Download the pretrained model:
[maskdino_swinl_50ep_300q_hid2048_3sd1_instance_maskenhanced_mask52.3ap_box59.0ap.pth](https://github.com/IDEA-Research/detrex-storage/releases/download/maskdino-v0.1.0/maskdino_swinl_50ep_300q_hid2048_3sd1_instance_maskenhanced_mask52.3ap_box59.0ap.pth)

## Training 
```sh
python train_net.py \
     --num-gpus 1 \
     --config-file configs/coco/instance-segmentation/swin/maskdino_R50_bs16_50ep_4s_dowsample1_2048.yaml \
     MODEL.WEIGHTS maskdino_swinl_50ep_300q_hid2048_3sd1_instance_maskenhanced_mask52.3ap_box59.0ap.pth
```
## Evaluation
```sh
python train_net.py \
     --eval-only \
     --num-gpus 1 \
     --config-file configs/coco/instance-segmentation/swin/maskdino_R50_bs16_50ep_4s_dowsample1_2048.yaml \
     DATASETS.TEST '("satellite_test",)' \
     MODEL.WEIGHTS "YOU_MODEL_CHECKPOINT_PATH"
```


## MapChallenge Instance Segmentation Results

| Model            | segm mAP | segm mAP@50 | segm mAP@75 | segm mAP_s | segm mAP_m | segm mAP_l | segm mAR | segm mAR@50 | segm mAR@75 |
|------------------|----------|-------------|-------------|------------|------------|------------|---------|--------|------------|
| SwinS-Mask2former| 0.3110   | 0.7160      | 0.2180      | 0.1690     | 0.4420     | 0.0990     | 0.42    | 0.833  | 0.362      |
| SwinL-Mask2former| 0.3080   | 0.7260      | 0.2360      | 0.1710     | 0.4400     | 0.1310     | 0.453   | 0.855  | 0.464      |
| Rtmdet-X         | 0.3910   | 0.7760      | 0.3440      | 0.2090     | 0.5440     | 0.2930     | 0.509   | 0.891  | 0.5        |
| RTMdet-M         | 0.3790   | 0.7540      | 0.3170      | 0.2150     | 0.5210     | 0.2820     | 0.485   |  0.87  | 0.457      |
| QueryInst-r50    | 0.2770   | 0.6520      | 0.1830      | 0.1380     | 0.3890     | 0.1530     | 0.432   | 0.826  | 0.384      |
| QueryInst-r101   | 0.2780   | 0.6340      | 0.2000      | 0.1760     | 0.3910     | 0.1010     | 0.458   | 0.855  | 0.464      |
| [**MaskDINO**](logs/experiment/maskdino-v2-full-run-1xH100-maskdino_R50_bs16_50ep_4s_dowsample1_2048.txt) | **58.3912**| **90.2239**| **61.4915**| **36.6915**| **69.1124**| **92.8676**| **68.0172**| **95.6897**| **75.0000**|


**Note:**
- **mAP@50/mAR@50** refers to average precision/recall at `IoU>=0.50` and **mAP@75/mAR@75** refers to average precision/recall at `IOU >= 0.75`.

- `segm mAP` values are usually averaged over multiple IOUs from 0.5 to 0.95 with interval of 0.05
- In metric columns,
       - `s` = small objects
       - `m` = medium objects
       - `l` = large objects

## Additional Usage
For full usage and detailed instructions, refer to [Detectron2 Getting Started Guide](https://github.com/facebookresearch/detectron2/blob/master/GETTING_STARTED.md).

## Related repositories
- [mmdetection training experiments ](https://github.com/saidineshpola/mapchallenge-instance-segmentation/tree/main)
