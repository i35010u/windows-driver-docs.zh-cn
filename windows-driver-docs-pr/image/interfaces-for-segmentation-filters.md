---
title: 分段筛选器的接口
description: 分段筛选器的接口
ms.assetid: 428f6fce-d76c-4485-aa92-39f2b608160d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e033ca9312ea22e0eff8b874f85504ea551b005b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358900"
---
# <a name="interfaces-for-segmentation-filters"></a>分段筛选器的接口





从 Windows Vista 开始，WIA 将支持分段的筛选器。 分段筛选器必须实现[IWiaSegmentationFilter 接口](https://msdn.microsoft.com/library/windows/hardware/ff545035)。

**IWiaSegmentationFilter**接口是依赖于新 （适用于 Windows Vista) 的界面**IWiaItem2**，在本部分中，用于为的超集**IWiaItem**. 除了**IWiaItem**方法， **IWiaItem2**接口包括方法**IWiaItem2::GetExtension**，用于应用程序创建 WIA扩展，其中包括分段筛选器。 **IWiaItem**并**IWiaItem2**接口 Microsoft Windows SDK 文档中所述。

**IWiaSegmentationFilter**接口实现单个方法**DetectRegions**。 此方法具有三个参数， *lFlags*， *pInputStream*，并*pWiaItem2*。

*LFlags*参数是当前未使用。

*PInputStream*参数是指向图像分段是要执行的。 这通常是表示平板的整个扫描曲面的预览图像。 中的应用程序创建流及其**IWiaTransferCallback::GetNextStream**方法; 此方法在图像采集过程中调用。 该驱动程序获取的映像将数据写入到流中的**IWiaTransferCallback::GetNextStream**方法返回。 这也是应传递到分段的筛选器应用程序的流。 **IWiaTransferCallback** Windows SDK 文档中详细介绍了接口。

*PWiaItem2*参数是指向为其的 WIA 项*pInputStream*已获取。 它也称为父项。 例如，项的*pWiaItem2*指向可能是平板项。

[ **IWiaSegmentationFilter::DetectRegions** ](https://msdn.microsoft.com/library/windows/hardware/ff545030)方法用于确定所表示的图像的子区域*pInputStream*。 有关检测到，每个子区域**IWiaSegmentationFilter::DetectRegions**创建新的子 WIA 项指向的项下*pWiaItem2*。 对于每个子项，分段的筛选器必须设置以下 WIA 属性的值：[**WIA\_IPS\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)， [ **WIA\_IP\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)， [ **WIA\_IPS\_大 XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)，并[ **WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)。 这些属性表示要扫描的区域的边框。 更高级的分段筛选器可能还想要设置其他 WIA 属性，如[分段的筛选器的 WIA 属性](wia-properties-for-segmentation-filters.md)驱动程序是否支持噪。

下图显示了如何细分筛选器修改应用程序项树。 在此图中，分段的筛选器已检测到在平板、 三个映像，并对于每个映像，它已创建新的子项目平板项下。

![说明如何细分筛选器修改应用程序项树的关系图](images/art-segmentation2.png)

分段筛选器必须支持它扩展了驱动程序支持的所有图像格式。 Microsoft 提供的分段筛选器支持 BMP、 GIF、 JPEG、 PNG 和 TIFF 格式。 因此，任何使用此筛选器的驱动程序被限制为这些格式。

若要创建子项目，分段筛选调用**IWiaItem2::CreateChildItem**方法。 下面是此类调用的示例：

```cpp
lItemFlags = WiaItemTypeGenerated | WiaItemTypeTransfer | WiaItemTypeImage | WiaItemTypeFile |
 WiaItemTypeProgrammableDataSource;

lCreationFlags = COPY_PARENT_PROPERTY_VALUES;

pWiaItem2->CreateChildItem(lItemFlags,
                           lCreationFlags,
                           bstrItemName,
                           &pChildItem);
```

**IWiaItem2::CreateChildItem**稍有不同**IWiaItem::CreateChildItem**。 **IWiaItem2::CreateChildItem**方法具有一个新的参数*lCreationFlags*;**IWiaItem2::CreateChildItem**方法的*lItemFlags*参数对应于*lFlags*参数**IWiaItem::CreateChildItem**。 传递复制\_父\_属性\_值替换*lCreationFlags* WIA 服务中，参数中前面的代码段中，所示指示 WIA 服务来设置所有可读/写WIA 的为相同的值作为其父级的子项目的属性。 分段筛选器应通过此标志的原因是为了确保属性，例如图像格式，并在新创建的子项目中，解析为父项。 因为范围设置的属性的分段的筛选器将到子项目依赖于图像的分辨率的解决方法是相同至关重要。 也很重要的映像格式和解决方法都是相同的子项中如果应用程序想要使用预览组件 （Microsoft Windows SDK 文档中所述）。 才会获取最终映像，应用程序可以修改获取扫描程序从更高质量的图像的分辨率。

请务必注意，通过它可以和不能执行中的应用程序相同的限制绑定分段筛选器。 这意味着应用程序可以修改分段筛选器创建的子项。 例如，用户可能不能满足与区域分段筛选器检测到并可能告知应用程序来修改此区域通过拖动它的角。 应用程序可以还删除分段筛选器创建的子项目，以及添加新的。

请注意，分段筛选器不负责"清理"它创建的子项目。 因此，如果应用程序调用**IWiaSegmentationFilter::DetectRegions**不止一次，应用程序必须先删除对的第一个调用中创建的子项目**IWiaSegmentationFilter::DetectRegions**方法。 分段的筛选器也不是负责重置*pInputStream*参数。 应用程序必须确保已将搜索指针设置到流的开头之前调用分段的筛选器。

电影项和平板项上，应仅使用分段的筛选器。 针对电影扫描，扫描程序通常提供固定帧，在这种情况下，驱动程序创建子项目 (请参阅[WIA 扫描程序项树布局](wia-scanner-item-tree-layout.md)有关详细信息)。 在这种情况下，应用程序不应调用创建的子项目和区域检测的分段筛选器。

如果驱动程序附带的分段的筛选器，它应实现[ **WIA\_IPS\_分段**](https://msdn.microsoft.com/library/windows/hardware/ff552649)其平板和电影胶片 WIA 项的属性。 此只读属性具有两个有效的值：WIA\_使用\_分段\_筛选器和 WIA\_不\_使用\_分段\_筛选器，该驱动程序设置。 此属性允许应用程序确定是否应为对某一项的区域检测使用驱动程序的分段的筛选器。

如果扫描仪的电影胶片扫描使用固定的帧，它会将此属性设置为 WIA\_不\_使用\_分段\_电影项中的筛选器。 在这种情况下，应用程序不应尝试加载分段的筛选器后已获取电影预览;相反，它应枚举驱动程序创建的子项目。 这些子项表示固定的帧。

因为 WIA 项传递到**IWiaSegmentationFilter::DetectRegions**，很可能使用不同的算法，具体取决于类别的项，即平板或电影的分段筛选器。 项的类别存储在[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性。

如果应用程序更改的任何属性*pWiaItem2*之间获取中的图像*pInputStream*以及对应用程序的调用**IWiaSegmentationFilter::DetectRegions**，必须还原原始属性设置 （即流已获取已有的项的属性设置）。 这可以使用**IWiaPropertyStorage::GetPropertyStream**并**IWiaPropertyStorage::SetPropertyStream**方法。 需要还原这些更改的原因是可能是 WIA 项所必需的分段的筛选器，但不是存储在映像标头中的信息。 此类信息的示例包括中存储的数据[ **WIA\_IPS\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)， [ **WIA\_IP\_YPOS** ](https://msdn.microsoft.com/library/windows/hardware/ff552671)，并[ **WIA\_IP\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff552648)属性。 **IWiaPropertyStorage** Windows SDK 文档中所述接口和其方法。

应用程序通过调用获取分段的筛选器的实例**IWiaItem2::GetExtension** （Windows SDK 文档中所述）。 应用程序通常会显示其预览窗口之前调用此方法。 这是因为驱动程序可能会不附带分段筛选器，用例 UI 应该知道不希望显示不受支持的按钮，如**执行分段**。

 

 




