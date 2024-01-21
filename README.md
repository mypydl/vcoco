# hico-det

# 主要特性

转换为 COCO 格式的 VCOCO 数据集标注，可用pycocotools.coco.COCO加载。

本仓库仅包含标注，图片下载参考文末[引用](#引用)。

ann_id遵循原本标注，但在[label_info.json](configs/label_info.json)中为其配置了valid_id，按照以下规则重新排列：

1. obj_name
2. verb_name

仅为了优化打印成表格后的视觉效果。

# 数据特性

- hoi: 260 (triplett)
- rel: 24 (排除 no-role-action 和 point-inter)
- obj: 80 (coco-ins)

# 标注格式

## image

```json
{
    'info': [...], 
    'licenses': [...], 
    'images': [
        {
            'file_name': 'HICO_test2015_00000001.jpg',
            'height'   : 427,
            'width'    : 640,
            'id'       : 1
        },
        ...
    ]
}
```

## instance

```json
{
    'info': [...], 
    'licenses': [...], 
    'images': [...],
    'annotations': [
        {
            'id'         : 1,
            'bbox'       : [320, 306, 39, 43],
            'area'       : 1677,
            'category_id': 1,
            'image_id'   : 1
        },
        ...
    ], 
    'categories': [
        {'supercategory': 'person', 'id': 1, 'name': 'person'},
        ...
    ]
}
```

## relation

```json
{
    'info': [...], 
    'licenses': [...], 
    'images': [...],
    'annotations': [
        {'id': 1, 'subject_id': 1, 'object_id': 3, 'category_id': 88, 'image_id': 1},
        ...
    ], 
    'categories': [
        {'id': 1, 'name': 'adjust'},
        ...
    ]
}
```

# 文件夹作用

## annotations

存放标注文件（coco格式）。

其中根目录的标注转换自[v-coco](https://github.com/s-gupta/v-coco)提供的标注文件。
而qpic子目录存放转换自[QPIC](https://arxiv.org/abs/2103.05399)提供的标注。

## tools

### base

建立标注和配置的过程，以及简易可视化（jupyter）。

### proposal

instance/person_keypoints预测的转化。

### text_embed

提取文本嵌入的脚本。

# 引用

论文: [Visual Semantic Role Labeling](http://arxiv.org/abs/1505.04474)

code: [https://github.com/s-gupta/v-coco](https://github.com/s-gupta/v-coco)
