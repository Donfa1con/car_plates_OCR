# car plates OCR

![Место](imgs/place.png?raw=true "Место")
![Место](imgs/subs.png?raw=true "Скор")

В качестве решения был взят бэйзлайн https://www.kaggle.com/alyar88/maskrcnn-bb-x-mask-crnn-0-53

Оно состоит из 3 частей:
 - Детекция номеров: maskrcnn_resnet50_fpn из torchvision
 - Вырезание и поворот 4-ех угольника
 - Распознавание номеров: RCNN с семинара (backbone resnet18)
 
В качестве аугментаций для детекции номеров добавлены albumentations:
 - A.ShiftScaleRotate(rotate_limit=10, border_mode=0)
 - A.IAAPerspective()
 - A.OneOf([A.HueSaturationValue(p=0.5), A.RGBShift(p=0.5)])
 - A.RandomBrightnessContrast(p=0.5)
 
Adam изменен на AdamW

Изменение ReduceLROnPlateau на CLR не улучшило скор на LB
