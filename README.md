基于torch实现水果目标检测的faster-RCNN

运行train.py 可能报错
TypeError: can't convert cuda:0 device type tensor to numpy. Use Tensor.cpu() to copy the tensor to host memory first.

模型只保存了对应的权重， 关于加载数据DataLoader中的 `num_workers=0` 根据自己的GPU可以提高。

模型有点大，Github放不了

```python
(base) ng@ng-Z390:~$ sudo vim /home/ng/.local/lib/python3.8/site-packages/torch/tensor.py

return self.numpy()
修改为：
return self.cpu().detach().numpy()
```




![](./image/fasterRCNN-___预测.png)

![](./image/fasterRCNN_设置阈值结果.png)



下面是10个epochs的训练结果


```python
Epoch: [0]  [ 0/20]  eta: 0:00:16  lr: 0.000268  loss: 1.5607 (1.5607)  loss_classifier: 1.2689 (1.2689)  loss_box_reg: 0.2748 (0.2748)  loss_objectness: 0.0094 (0.0094)  loss_rpn_box_reg: 0.0076 (0.0076)  time: 0.8476  data: 0.0907  max mem: 7153
Epoch: [0]  [10/20]  eta: 0:00:08  lr: 0.002897  loss: 0.9007 (0.9959)  loss_classifier: 0.5513 (0.6719)  loss_box_reg: 0.2997 (0.3108)  loss_objectness: 0.0064 (0.0062)  loss_rpn_box_reg: 0.0063 (0.0071)  time: 0.8516  data: 0.0973  max mem: 7419
Epoch: [0]  [19/20]  eta: 0:00:00  lr: 0.005000  loss: 0.6107 (0.7333)  loss_classifier: 0.3075 (0.4568)  loss_box_reg: 0.2437 (0.2643)  loss_objectness: 0.0064 (0.0064)  loss_rpn_box_reg: 0.0053 (0.0059)  time: 0.8256  data: 0.0978  max mem: 7419
Epoch: [0] Total time: 0:00:16 (0.8257 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3247 (0.3247)  evaluator_time: 0.0185 (0.0185)  time: 0.4038  data: 0.0486  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3190 (0.3086)  evaluator_time: 0.0178 (0.0178)  time: 0.3975  data: 0.0593  max mem: 7419
Test: Total time: 0:00:01 (0.3976 s / it)
Averaged stats: model_time: 0.3190 (0.3086)  evaluator_time: 0.0178 (0.0178)
Accumulating evaluation results...
DONE (t=0.02s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.182
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.390
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.139
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.182
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.214
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.458
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.504
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.504
Epoch: [1]  [ 0/20]  eta: 0:00:16  lr: 0.005000  loss: 0.3089 (0.3089)  loss_classifier: 0.1170 (0.1170)  loss_box_reg: 0.1753 (0.1753)  loss_objectness: 0.0072 (0.0072)  loss_rpn_box_reg: 0.0094 (0.0094)  time: 0.8436  data: 0.0792  max mem: 7419
Epoch: [1]  [10/20]  eta: 0:00:08  lr: 0.005000  loss: 0.3829 (0.3750)  loss_classifier: 0.1384 (0.1382)  loss_box_reg: 0.2252 (0.2186)  loss_objectness: 0.0085 (0.0103)  loss_rpn_box_reg: 0.0078 (0.0080)  time: 0.8673  data: 0.1014  max mem: 7419
Epoch: [1]  [19/20]  eta: 0:00:00  lr: 0.005000  loss: 0.3826 (0.3880)  loss_classifier: 0.1381 (0.1417)  loss_box_reg: 0.2252 (0.2307)  loss_objectness: 0.0072 (0.0085)  loss_rpn_box_reg: 0.0063 (0.0071)  time: 0.8350  data: 0.0976  max mem: 7419
Epoch: [1] Total time: 0:00:16 (0.8350 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3288 (0.3288)  evaluator_time: 0.0134 (0.0134)  time: 0.4018  data: 0.0474  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3206 (0.3110)  evaluator_time: 0.0128 (0.0126)  time: 0.3946  data: 0.0593  max mem: 7419
Test: Total time: 0:00:01 (0.3947 s / it)
Averaged stats: model_time: 0.3206 (0.3110)  evaluator_time: 0.0128 (0.0126)
Accumulating evaluation results...
DONE (t=0.02s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.305
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.672
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.157
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.305
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.260
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.499
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.511
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.511
Epoch: [2]  [ 0/20]  eta: 0:00:17  lr: 0.005000  loss: 0.3346 (0.3346)  loss_classifier: 0.1223 (0.1223)  loss_box_reg: 0.1987 (0.1987)  loss_objectness: 0.0057 (0.0057)  loss_rpn_box_reg: 0.0079 (0.0079)  time: 0.8582  data: 0.0900  max mem: 7419
Epoch: [2]  [10/20]  eta: 0:00:08  lr: 0.005000  loss: 0.3048 (0.3239)  loss_classifier: 0.1143 (0.1228)  loss_box_reg: 0.1808 (0.1887)  loss_objectness: 0.0053 (0.0059)  loss_rpn_box_reg: 0.0064 (0.0064)  time: 0.8644  data: 0.0941  max mem: 7419
Epoch: [2]  [19/20]  eta: 0:00:00  lr: 0.005000  loss: 0.3048 (0.3132)  loss_classifier: 0.1160 (0.1216)  loss_box_reg: 0.1714 (0.1811)  loss_objectness: 0.0033 (0.0044)  loss_rpn_box_reg: 0.0058 (0.0061)  time: 0.8373  data: 0.0953  max mem: 7419
Epoch: [2] Total time: 0:00:16 (0.8373 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:01  model_time: 0.3283 (0.3283)  evaluator_time: 0.0097 (0.0097)  time: 0.3981  data: 0.0479  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3215 (0.3114)  evaluator_time: 0.0090 (0.0092)  time: 0.3920  data: 0.0595  max mem: 7419
Test: Total time: 0:00:01 (0.3921 s / it)
Averaged stats: model_time: 0.3215 (0.3114)  evaluator_time: 0.0090 (0.0092)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.435
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.818
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.381
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.436
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.334
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.560
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.567
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.567
Epoch: [3]  [ 0/20]  eta: 0:00:20  lr: 0.000500  loss: 0.2005 (0.2005)  loss_classifier: 0.0737 (0.0737)  loss_box_reg: 0.1206 (0.1206)  loss_objectness: 0.0017 (0.0017)  loss_rpn_box_reg: 0.0046 (0.0046)  time: 1.0179  data: 0.2455  max mem: 7419
Epoch: [3]  [10/20]  eta: 0:00:08  lr: 0.000500  loss: 0.2473 (0.2379)  loss_classifier: 0.0997 (0.0911)  loss_box_reg: 0.1422 (0.1384)  loss_objectness: 0.0022 (0.0028)  loss_rpn_box_reg: 0.0055 (0.0057)  time: 0.8723  data: 0.0990  max mem: 7419
Epoch: [3]  [19/20]  eta: 0:00:00  lr: 0.000500  loss: 0.2321 (0.2349)  loss_classifier: 0.0939 (0.0904)  loss_box_reg: 0.1236 (0.1358)  loss_objectness: 0.0022 (0.0036)  loss_rpn_box_reg: 0.0046 (0.0052)  time: 0.8395  data: 0.0950  max mem: 7419
Epoch: [3] Total time: 0:00:16 (0.8395 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:01  model_time: 0.3251 (0.3251)  evaluator_time: 0.0095 (0.0095)  time: 0.3953  data: 0.0484  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3223 (0.3112)  evaluator_time: 0.0088 (0.0087)  time: 0.3914  data: 0.0598  max mem: 7419
Test: Total time: 0:00:01 (0.3915 s / it)
Averaged stats: model_time: 0.3223 (0.3112)  evaluator_time: 0.0088 (0.0087)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.471
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.844
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.456
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.472
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.359
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.599
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.605
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.605
Epoch: [4]  [ 0/20]  eta: 0:00:19  lr: 0.000500  loss: 0.2154 (0.2154)  loss_classifier: 0.0816 (0.0816)  loss_box_reg: 0.1281 (0.1281)  loss_objectness: 0.0023 (0.0023)  loss_rpn_box_reg: 0.0034 (0.0034)  time: 0.9898  data: 0.2163  max mem: 7419
Epoch: [4]  [10/20]  eta: 0:00:08  lr: 0.000500  loss: 0.2154 (0.2281)  loss_classifier: 0.0816 (0.0889)  loss_box_reg: 0.1281 (0.1315)  loss_objectness: 0.0023 (0.0029)  loss_rpn_box_reg: 0.0036 (0.0049)  time: 0.8830  data: 0.1062  max mem: 7419
Epoch: [4]  [19/20]  eta: 0:00:00  lr: 0.000500  loss: 0.2154 (0.2277)  loss_classifier: 0.0777 (0.0873)  loss_box_reg: 0.1281 (0.1328)  loss_objectness: 0.0023 (0.0029)  loss_rpn_box_reg: 0.0046 (0.0048)  time: 0.8422  data: 0.0946  max mem: 7419
Epoch: [4] Total time: 0:00:16 (0.8423 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3367 (0.3367)  evaluator_time: 0.0095 (0.0095)  time: 0.4065  data: 0.0481  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3221 (0.3135)  evaluator_time: 0.0081 (0.0085)  time: 0.3931  data: 0.0593  max mem: 7419
Test: Total time: 0:00:01 (0.3932 s / it)
Averaged stats: model_time: 0.3221 (0.3135)  evaluator_time: 0.0081 (0.0085)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.504
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.861
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.574
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.504
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.380
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.611
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.616
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.616
Epoch: [5]  [ 0/20]  eta: 0:00:17  lr: 0.000500  loss: 0.1495 (0.1495)  loss_classifier: 0.0670 (0.0670)  loss_box_reg: 0.0775 (0.0775)  loss_objectness: 0.0029 (0.0029)  loss_rpn_box_reg: 0.0021 (0.0021)  time: 0.8528  data: 0.0758  max mem: 7419
Epoch: [5]  [10/20]  eta: 0:00:08  lr: 0.000500  loss: 0.2151 (0.2067)  loss_classifier: 0.0800 (0.0806)  loss_box_reg: 0.1227 (0.1189)  loss_objectness: 0.0025 (0.0028)  loss_rpn_box_reg: 0.0043 (0.0044)  time: 0.8731  data: 0.0970  max mem: 7419
Epoch: [5]  [19/20]  eta: 0:00:00  lr: 0.000500  loss: 0.2181 (0.2065)  loss_classifier: 0.0800 (0.0779)  loss_box_reg: 0.1265 (0.1215)  loss_objectness: 0.0022 (0.0026)  loss_rpn_box_reg: 0.0043 (0.0044)  time: 0.8435  data: 0.0956  max mem: 7419
Epoch: [5] Total time: 0:00:16 (0.8436 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3401 (0.3401)  evaluator_time: 0.0102 (0.0102)  time: 0.4102  data: 0.0477  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3216 (0.3150)  evaluator_time: 0.0076 (0.0082)  time: 0.3942  data: 0.0593  max mem: 7419
Test: Total time: 0:00:01 (0.3943 s / it)
Averaged stats: model_time: 0.3216 (0.3150)  evaluator_time: 0.0076 (0.0082)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.512
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.865
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.568
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.512
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.374
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.628
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.630
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.630
Epoch: [6]  [ 0/20]  eta: 0:00:19  lr: 0.000050  loss: 0.1489 (0.1489)  loss_classifier: 0.0464 (0.0464)  loss_box_reg: 0.0957 (0.0957)  loss_objectness: 0.0009 (0.0009)  loss_rpn_box_reg: 0.0059 (0.0059)  time: 0.9663  data: 0.1916  max mem: 7419
Epoch: [6]  [10/20]  eta: 0:00:08  lr: 0.000050  loss: 0.1850 (0.1964)  loss_classifier: 0.0731 (0.0741)  loss_box_reg: 0.1148 (0.1152)  loss_objectness: 0.0033 (0.0033)  loss_rpn_box_reg: 0.0033 (0.0038)  time: 0.8638  data: 0.0870  max mem: 7419
Epoch: [6]  [19/20]  eta: 0:00:00  lr: 0.000050  loss: 0.1850 (0.2033)  loss_classifier: 0.0731 (0.0759)  loss_box_reg: 0.1090 (0.1203)  loss_objectness: 0.0018 (0.0028)  loss_rpn_box_reg: 0.0037 (0.0043)  time: 0.8444  data: 0.0954  max mem: 7419
Epoch: [6] Total time: 0:00:16 (0.8445 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3260 (0.3260)  evaluator_time: 0.0349 (0.0349)  time: 0.4206  data: 0.0475  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3219 (0.3115)  evaluator_time: 0.0078 (0.0132)  time: 0.3961  data: 0.0595  max mem: 7419
Test: Total time: 0:00:01 (0.3962 s / it)
Averaged stats: model_time: 0.3219 (0.3115)  evaluator_time: 0.0078 (0.0132)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.516
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.872
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.587
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.517
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.379
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.634
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.636
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.636
Epoch: [7]  [ 0/20]  eta: 0:00:18  lr: 0.000050  loss: 0.2391 (0.2391)  loss_classifier: 0.0885 (0.0885)  loss_box_reg: 0.1421 (0.1421)  loss_objectness: 0.0046 (0.0046)  loss_rpn_box_reg: 0.0039 (0.0039)  time: 0.9317  data: 0.1590  max mem: 7419
Epoch: [7]  [10/20]  eta: 0:00:08  lr: 0.000050  loss: 0.2152 (0.2001)  loss_classifier: 0.0805 (0.0764)  loss_box_reg: 0.1250 (0.1176)  loss_objectness: 0.0017 (0.0027)  loss_rpn_box_reg: 0.0035 (0.0034)  time: 0.8809  data: 0.0997  max mem: 7419
Epoch: [7]  [19/20]  eta: 0:00:00  lr: 0.000050  loss: 0.2097 (0.2035)  loss_classifier: 0.0790 (0.0763)  loss_box_reg: 0.1250 (0.1195)  loss_objectness: 0.0028 (0.0034)  loss_rpn_box_reg: 0.0037 (0.0043)  time: 0.8470  data: 0.0961  max mem: 7419
Epoch: [7] Total time: 0:00:16 (0.8471 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3417 (0.3417)  evaluator_time: 0.0093 (0.0093)  time: 0.4112  data: 0.0481  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3231 (0.3151)  evaluator_time: 0.0075 (0.0081)  time: 0.3948  data: 0.0599  max mem: 7419
Test: Total time: 0:00:01 (0.3950 s / it)
Averaged stats: model_time: 0.3231 (0.3151)  evaluator_time: 0.0075 (0.0081)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.520
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.860
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.603
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.521
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.382
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.639
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.641
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.641
Epoch: [8]  [ 0/20]  eta: 0:00:17  lr: 0.000050  loss: 0.1979 (0.1979)  loss_classifier: 0.0671 (0.0671)  loss_box_reg: 0.1219 (0.1219)  loss_objectness: 0.0047 (0.0047)  loss_rpn_box_reg: 0.0041 (0.0041)  time: 0.8664  data: 0.0852  max mem: 7419
Epoch: [8]  [10/20]  eta: 0:00:08  lr: 0.000050  loss: 0.2060 (0.2270)  loss_classifier: 0.0784 (0.0851)  loss_box_reg: 0.1219 (0.1339)  loss_objectness: 0.0022 (0.0033)  loss_rpn_box_reg: 0.0043 (0.0048)  time: 0.8654  data: 0.0841  max mem: 7419
Epoch: [8]  [19/20]  eta: 0:00:00  lr: 0.000050  loss: 0.1979 (0.2075)  loss_classifier: 0.0697 (0.0766)  loss_box_reg: 0.1213 (0.1238)  loss_objectness: 0.0020 (0.0025)  loss_rpn_box_reg: 0.0035 (0.0045)  time: 0.8471  data: 0.0953  max mem: 7419
Epoch: [8] Total time: 0:00:16 (0.8471 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3373 (0.3373)  evaluator_time: 0.0091 (0.0091)  time: 0.4070  data: 0.0485  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3237 (0.3150)  evaluator_time: 0.0078 (0.0081)  time: 0.3946  data: 0.0598  max mem: 7419
Test: Total time: 0:00:01 (0.3947 s / it)
Averaged stats: model_time: 0.3237 (0.3150)  evaluator_time: 0.0078 (0.0081)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.521
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.860
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.615
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.522
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.381
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.642
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.644
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.644
Epoch: [9]  [ 0/20]  eta: 0:00:17  lr: 0.000005  loss: 0.1285 (0.1285)  loss_classifier: 0.0512 (0.0512)  loss_box_reg: 0.0734 (0.0734)  loss_objectness: 0.0008 (0.0008)  loss_rpn_box_reg: 0.0030 (0.0030)  time: 0.8589  data: 0.0866  max mem: 7419
Epoch: [9]  [10/20]  eta: 0:00:08  lr: 0.000005  loss: 0.2507 (0.2274)  loss_classifier: 0.0872 (0.0829)  loss_box_reg: 0.1445 (0.1365)  loss_objectness: 0.0016 (0.0035)  loss_rpn_box_reg: 0.0046 (0.0044)  time: 0.8794  data: 0.0961  max mem: 7419
Epoch: [9]  [19/20]  eta: 0:00:00  lr: 0.000005  loss: 0.1916 (0.2006)  loss_classifier: 0.0762 (0.0749)  loss_box_reg: 0.1110 (0.1183)  loss_objectness: 0.0016 (0.0029)  loss_rpn_box_reg: 0.0039 (0.0044)  time: 0.8487  data: 0.0950  max mem: 7419
Epoch: [9] Total time: 0:00:16 (0.8488 s / it)
creating index...
index created!
Test:  [0/5]  eta: 0:00:02  model_time: 0.3328 (0.3328)  evaluator_time: 0.0099 (0.0099)  time: 0.4024  data: 0.0476  max mem: 7419
Test:  [4/5]  eta: 0:00:00  model_time: 0.3242 (0.3142)  evaluator_time: 0.0076 (0.0082)  time: 0.3935  data: 0.0593  max mem: 7419
Test: Total time: 0:00:01 (0.3936 s / it)
Averaged stats: model_time: 0.3242 (0.3142)  evaluator_time: 0.0076 (0.0082)
Accumulating evaluation results...
DONE (t=0.01s).
IoU metric: bbox
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.523
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.860
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.615
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.523
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.381
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.644
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.645
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.645
```