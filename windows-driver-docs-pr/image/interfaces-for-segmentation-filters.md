---
title: 分段筛选器的接口
description: 分段筛选器的接口
ms.assetid: 428f6fce-d76c-4485-aa92-39f2b608160d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10089345d2d4d2bef7fe4300c55131a694e5e981
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192289"
---
# <a name="interfaces-for-segmentation-filters"></a>分段筛选器的接口





从 Windows Vista 开始，WIA 将支持分段筛选器。 分段筛选器必须实现 [IWiaSegmentationFilter 接口](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter)。

**IWiaSegmentationFilter**接口依赖于 Windows Vista 的新 () interface **IWiaItem2**，此部分在本部分中使用，是**IWiaItem**的超集。 除了 **IWiaItem** 方法， **IWiaItem2** 接口还包含方法 **IWiaItem2：： path.getextension 对**，应用程序使用该方法来创建 WIA 扩展，包括分段筛选器。 Microsoft Windows SDK 文档中介绍了 **IWiaItem** 和 **IWiaItem2** 接口。

**IWiaSegmentationFilter**接口实现了单一方法**DetectRegions**。 此方法有三个参数： *lFlags*、 *pInputStream*和 *pWiaItem2*。

*LFlags*参数当前未使用。

*PInputStream*参数是一个指针，指向要在其上执行分段的图像。 通常，这是表示平板的整个扫描表面的预览图像。 流是由应用程序在其 **IWiaTransferCallback：： GetNextStream** 方法中创建的;此方法在图像获取过程中调用。 驱动程序将获取的图像数据写入到 **IWiaTransferCallback：： GetNextStream** 方法返回的流中。 这也是应用程序应传递到分段筛选器中的流。 Windows SDK 文档中介绍了 **IWiaTransferCallback** 接口。

*PWiaItem2*参数是指向为其获取*pInputStream*的 WIA 项的指针。 它也称为父项。 例如， *pWiaItem2* 指向的项可以是 "平台" 项。

[**IWiaSegmentationFilter：:D etectregions**](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiasegmentationfilter-detectregions)方法用于确定*pInputStream*表示的图像的子区域。 对于检测到的每个子区域， **IWiaSegmentationFilter：:D etectregions** 将在 *pWiaItem2*指向的项下创建新的子 WIA 项。 对于每个子项，分段筛选器必须设置以下 WIA 属性的值： [**wia \_ ips \_ XPOS**](./wia-ips-xpos.md)、 [**wia \_ ip \_ YPOS**](./wia-ips-ypos.md)、 [**wia \_ ips \_ XEXTENT**](./wia-ips-xextent.md)和 [**wia \_ ips \_ YEXTENT**](./wia-ips-yextent.md)。 这些属性表示要扫描的区域的边框。 如果驱动程序支持 deskewing，更高级的分段筛选器可能还需要设置其他 WIA 属性，如 [分段筛选器的 Wia 属性](wia-properties-for-segmentation-filters.md) 。

下图显示了分段筛选器如何修改应用程序项树。 在此图中，分段筛选器已在平板上检测到三个图像，对于每个图像，它在 "平台" 项下创建了一个新的子项。

![阐释分段筛选器如何修改应用程序项树的关系图](images/art-segmentation2.png)

分段筛选器必须支持它所扩展的驱动程序支持的所有映像格式。 Microsoft 提供的分段筛选器支持 BMP、GIF、JPEG、PNG 和 TIFF 格式。 因此，使用此筛选器的任何驱动程序都被限制为这些格式。

若要创建子项目，分段筛选器将调用 **IWiaItem2：： CreateChildItem** 方法。 下面是此类调用的一个示例：

```cpp
lItemFlags = WiaItemTypeGenerated | WiaItemTypeTransfer | WiaItemTypeImage | WiaItemTypeFile |
 WiaItemTypeProgrammableDataSource;

lCreationFlags = COPY_PARENT_PROPERTY_VALUES;

pWiaItem2->CreateChildItem(lItemFlags,
                           lCreationFlags,
                           bstrItemName,
                           &pChildItem);
```

**IWiaItem2：： CreateChildItem** 与 **IWiaItem：： CreateChildItem**略有不同。 **IWiaItem2：： CreateChildItem**方法有一个新参数*lCreationFlags*;**IWiaItem2：： CreateChildItem**方法的*lItemFlags*参数对应于**IWiaItem：： CreateChildItem**的*lFlags*参数。 \_ \_ \_ 如前面的代码段所示，将复制父属性值与*lCreationFlags*参数一起传递给 wia 服务，通知 wia 服务将子项的所有可读/可写 WIA 属性设置为与其父级相同的值。 分段筛选器应传递此标志的原因是确保新创建的子项目中的属性（如图像格式和分辨率）作为父项。 这一点很重要，因为分段筛选器将设置到子项的区属性取决于图像的分辨率。 如果应用程序想要使用 Microsoft Windows SDK 文档) 中所述 (预览组件，则子项目中的图像格式和分辨率也是相同的。 在获取最终映像之前，应用程序可以修改分辨率以从扫描仪获取更高质量的图像。

需要注意的是，分段筛选器与应用程序在它可以和不能执行的操作上绑定的限制相同。 这意味着应用程序可以修改分段筛选器创建的子项。 例如，用户可能对分段筛选器检测到的区域不满意，并且可能会告诉应用程序通过拖动其角来修改此区域。 应用程序还可以删除由分段筛选器创建的子项，还可以添加新的子项目。

请注意，分段筛选器不负责 "清除" 它创建的子项。 因此，如果应用程序多次调用 **IWiaSegmentationFilter：:D etectregions** ，应用程序必须首先删除在第一次调用 **IWiaSegmentationFilter：:D etectregions** 方法时创建的子项目。 分段筛选器也不负责重置 *pInputStream* 参数。 在调用分段筛选器之前，应用程序必须确保已将查找指针设置到流的开始位置。

分段筛选器只应在电影项目和平板项目上使用。 对于胶片扫描，扫描仪通常附带固定帧，在这种情况下，驱动程序将创建子项 (请参阅 [WIA 扫描器项树布局](wia-scanner-item-tree-layout.md) 了解详细信息) 。 在这种情况下，应用程序不应调用分段筛选器来检测和创建子项目。

如果驱动程序附带分段筛选器，它应为其平板和胶卷 WIA 项实现 [**WIA \_ IPS \_ 分段**](./wia-ips-segmentation.md) 属性。 此只读属性具有两个有效值： WIA \_ 使用 \_ 分段 \_ 筛选器和 WIA \_ 不要 \_ 使用 \_ \_ 驱动程序设置的分段筛选器。 此属性可让应用程序知道它是否应该使用驱动程序的分段筛选器来检测特定项的区域。

如果扫描程序使用固定帧进行胶片扫描，则会将此属性设置为 WIA，而不会 \_ \_ \_ \_ 在胶卷项中使用分段筛选器。 在这种情况下，应用程序不应在获取了胶片预览后尝试加载分段筛选器;相反，它应枚举由驱动程序创建的子项目。 这些子项表示固定的帧。

由于 WIA 项会传递到 **IWiaSegmentationFilter 中：:D etectregions**，因此，分段筛选器可能会根据项的类别（即平板或胶片）使用不同的算法。 项的类别存储在 [**WIA \_ IPA \_ item \_ category**](./wia-ipa-item-category.md) 属性中。

如果应用程序在*pInputStream*中获取映像和应用程序对**IWiaSegmentationFilter：:D etectregions**的调用之间更改了*pWiaItem2*中的任何属性，则原始属性设置 (例如，在获取流时该项目具有的属性设置) 必须还原。 可以使用 **IWiaPropertyStorage：： GetPropertyStream** 和 **IWiaPropertyStorage：： SetPropertyStream** 方法完成此操作。 需要还原这些更改的原因是，在分段筛选器所需的 WIA 项中可能存在信息，但这些信息并不存储在图像标头中。 此类信息的示例包括 [**wia \_ ip \_ XPOS**](./wia-ips-xpos.md)、 [**wia \_ ip \_ YPOS**](./wia-ips-ypos.md)和 [**wia \_ ips \_ 旋转**](./wia-ips-rotation.md) 属性中存储的数据。 Windows SDK 文档中介绍了 **IWiaPropertyStorage** 接口及其方法。

应用程序通过调用 Windows SDK 文档) 中所述的 **IWiaItem2：： path.getextension 对** (获取分段筛选器的实例。 在显示其预览窗口之前，应用程序通常会调用此方法。 这是因为，驱动程序可能不附带分段筛选器，在这种情况下，UI 应知道不会显示不受支持的按钮，例如 **执行分段**。

 

