---
title: WIA 项标志和类别的示例用法
description: WIA 项标志和类别的示例用法
ms.assetid: 8c9f7d85-6c84-4df9-9db3-6554d7eddf93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab70a556e0001eb548dea2477a39febfce77a62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375045"
---
# <a name="example-usage-of-wia-item-flags-and-categories"></a>WIA 项标志和类别的示例用法





本主题适用于 Windows Vista 和更高版本。

本部分描述了扫描仪和照相机项树在 Windows Vista 中，以及 WIA 项标志和 WIA 类别。 在关系图描绘了什么照相机项树和扫描程序项树如下所示在 Windows Vista 及更高版本。 有摄像机项树和扫描程序项树的两个关系图。 在这两种情况下，第一个关系图说明了所需的 WIA 项标志，虽然第二个关系图阐释了将使用哪个 WIA 类别。 代码示例是应用程序将如何使用的标志和类别组合的示例。

下图显示了照相机项树和标志中 WIA\_项\_标志必须设置的属性。

![说明具有 wia 项标志的照相机树关系图](images/art-film-tree1.png)

在上图中，在左侧的树表示照相机项树。 在右侧的批注框包含此类设备将需要使用 WIA 项标志。

下图显示了照相机项树和类别中 WIA\_IPA\_项\_类别属性必须设置的。

![说明显示类别的照相机树关系图](images/art-film-tree2.png)

在上图中，在左侧的树表示照相机项树。 在右侧气球中含有此类设备将需要使用的类别。

下图显示具有文档送纸器的扫描仪和电影胶片扫描仪和标志的项树中 WIA\_项\_标志必须设置的属性。

![说明具有文档送纸器的扫描仪和电影胶片扫描仪和 wia 项标志项树的关系图](images/art-flatbed-tree1.png)

在上图中，在左侧的树表示扫描程序项树。 在右侧的批注框包含此类设备将需要使用 WIA 项标志。

下图显示一个扫描程序，并将类别的项树中 WIA\_IPA\_项\_类别属性必须设置的。

![说明一个扫描程序，以及必须设置的类别的项树的关系图](images/art-flatbed-tree2.png)

在上图中，在左侧的树表示扫描程序项树。 在右侧的批注框包含中 WIA 的类别\_IPA\_项\_必须设置此类设备的 CATEGORY 属性。

由 WIA 和有关每个类别的有效 WIA 项标志的信息定义的所有类别的完整列表，请参阅[ **WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)。

有关所有 WIA 的完整列表项标记请参阅[ **WIA\_IPA\_项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)。

下面的代码示例演示了如何应用程序可以使用 WIA 的组合\_IPA\_项\_标志和 WIA\_IPA\_项\_类别进行分类的属性WIA 项树中发现项 WIA。

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

 

 




