---
title: WIA 项标志和类别的示例用法
description: WIA 项标志和类别的示例用法
ms.assetid: 8c9f7d85-6c84-4df9-9db3-6554d7eddf93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 176cf4fdd9c0e94b9e545eee9706ecb601e39ad6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192093"
---
# <a name="example-usage-of-wia-item-flags-and-categories"></a>WIA 项标志和类别的示例用法





本主题适用于 Windows Vista 和更高版本。

本部分介绍了 Windows Vista 中的扫描仪和照相机项树以及 WIA 项标志和 WIA 类别。 关系图显示了在 Windows Vista 和更高版本中，照相机项树和扫描仪项树的外观。 "相机项树" 和 "扫描仪项" 树有两个关系图。 在这两种情况下，第一个关系图说明了需要哪些 WIA 项标志，而第二个关系图说明了所使用的 WIA 类别。 此代码示例是应用程序为使用标志和类别组合而执行的操作的示例。

下图显示了必须设置的 "WIA \_ 项" 标志属性中的 "照相机" 项树和标志 \_ 。

![阐释带有 wia 项标志的相机树的关系图](images/art-film-tree1.png)

在上图中，左侧的树表示相机项树。 右侧的气球包含了此类设备需要使用的 WIA 项标志。

下图显示了必须设置的 "WIA \_ IPA \_ 项类别" 属性中的 "照相机" 项树和类别 \_ 。

![说明显示类别的相机树的关系图](images/art-film-tree2.png)

在上图中，左侧的树表示相机项树。 右侧的气球包含此类设备需要使用的类别。

下图显示了具有文档送纸器和胶卷扫描器的扫描仪的项目树，以及 \_ 必须设置的 WIA 项 flags 属性中的标志 \_ 。

![说明具有文档送纸器和胶卷扫描器的扫描仪的项目树的关系图，以及 wia 项标志](images/art-flatbed-tree1.png)

在上图中，左侧的树表示扫描器项树。 右侧的气球包含了此类设备需要使用的 WIA 项标志。

下图显示了扫描仪的项树以及 \_ 必须设置的 WIA IPA \_ 项类别属性中的类别 \_ 。

![说明扫描仪的项树以及必须设置的类别的关系图](images/art-flatbed-tree2.png)

在上图中，左侧的树表示扫描器项树。 右侧的气球包含 WIA \_ IPA ITEM CATEGORY 属性中的类别 \_ \_ ，此类设备必须设置此类属性。

有关 WIA 定义的所有类别的完整列表，以及每个类别的有效 WIA 项标志的信息，请参阅 [**WIA \_ IPA \_ item \_ category**](./wia-ipa-item-category.md)。

有关所有 WIA 项标志的完整列表，请参阅 [**WIA \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

下面的代码示例演示应用程序如何使用 WIA \_ IPA \_ item \_ 标志和 wia \_ IPA \_ 项 \_ 类别属性组合来分类 wia 项树中的 wia 项。

```cpp
HRESULT hr = S_OK;
PROPSPEC ps[2] = {{PRSPEC_PROPID,WIA_IPA_ITEM_FLAGS},
                  {PRSPEC_PROPID, WIA_IPA_ITEM_CATEGORY}};
PROPVARIANT pv[2] = {0};

hr = pIWiaPropertyStorage->ReadMultiple(2, ps, pv);
if (hr == S_OK)
{
    if (pv[0].lVal & WiaItemTypeProgrammableDataSource)
    {
        // Item is a programmable data source.
    }
    else
    {
        // Item is NOT a programmable data source and there must be
        // some data associated with the device, or a folder.
        // Use the WIA item flags to further classify the item.

        if (pv[0].lVal & WiaItemTypeImage)
        {
            // Item represents image data.
        }
        if (pv[0].lVal & WiaItemTypeAudio)
        {
            // Item represents audio data.
        }
        if (pv[0].lVal & WiaItemTypeVideo)
        {
            // Item represents video data.
        }
        if (pv[0].lVal & WiaItemTypeDocument)
        {
            // Item represents document data.
        }
    }

    // Read the category to properly use the item.
    switch(pv[1].lVal)
    {
        case WIA_CATEGORY_FINISHED_FILE:
            // Item is a finished file item.
  break;
        case WIA_CATEGORY_FLATBED:
            // Item is a flatbed scanner item.
   break;
        case WIA_CATEGORY_FILM:
            // Item is a film scanning item.
  break;
        case WIA_CATEGORY_FEEDER:
            // Item is a document feeder scanner item.
   break;
        default:
            // Item is not a WIA-defined item (possibly vendor specific?).
   break;
    }
    ...
}
...
```

 

