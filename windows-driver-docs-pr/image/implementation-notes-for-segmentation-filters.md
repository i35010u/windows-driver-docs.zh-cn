---
title: 分段筛选器的实现说明
description: 分段筛选器的实现说明
ms.assetid: c4caf8dd-8108-4bc7-b02f-1e180fedb95f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf16aa98cdf822a039ed993a532bae23a9ef181d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191905"
---
# <a name="implementation-notes-for-segmentation-filters"></a>分段筛选器的实现说明





请务必注意，分段筛选器设置为其创建的每个子项的属性。 这些属性包括： [**wia \_ ip \_ XPOS**](./wia-ips-xpos.md)、 [**wia \_ ip \_ YPOS**](./wia-ips-ypos.md)、 [**wia \_ Ips \_ XEXTENT**](./wia-ips-xextent.md)、wia \_ ips \_ YEXTENT，以及可能的 [**wia \_ ip \_ 反扭曲 \_ X**](./wia-ips-deskew-x.md) 和 [**wia \_ ip \_ 抗扭反 \_ Y**](./wia-ips-deskew-y.md)。 这些属性值对应于平台上项的位置，而不是传递到 *pInputStream* 参数中的图像。

因此，分段筛选器必须密切注意所 \_ 传入映像的 wia ip \_ XPOS、wia \_ Ip \_ YPOS 和 [**wia \_ ip \_ 旋转**](./wia-ips-rotation.md) 属性，这一点非常重要。

例如，假设应用程序进行预览扫描，在获取预览图像之前，应用程序会将 WIA \_ ip \_ XPOS = wia \_ ip \_ YPOS = 200 到 (父) 项。 然后，它调用分段筛选器来检测可能的子区域。 但是，分段筛选器中使用的实际算法作用于传入它的映像。 如果此算法检测到图像左边缘右侧为150像素，从图像顶部向下200像素，这实际上对应于扫描仪上 (350，400) 上的一个点。

在下图中，外部区域表示扫描仪平台。 尽管该算法将查找要 (150，200) 的区域左上角的坐标，但分段筛选器应设置为 WIA \_ ip XPOS 和 wia ip YPOS 的子项目的值为 \_ \_ \_ 350 和400。

![说明应用到部分影印的分段筛选器的关系图](images/art-segmentation3.png)

例如，如果应用程序将以可视方式显示分段筛选器检测到的区域，则必须注意，分段筛选器将设置与其在平板中的位置相对应的坐标。 这意味着应用程序必须将平板坐标映射到预览图像中的坐标。 但在大多数情况下，应用程序将使用 WIA \_ ip \_ XPOS = wia \_ ip \_ YPOS = 0 执行预览扫描，而不会旋转 ([**WIA \_ ip \_ 旋转**](./wia-ips-rotation.md) = 纵向) 。 如果是这种情况，则平台上的坐标与预览图像中的坐标之间存在直接的映射。

分段筛选器必须注意的另一个属性是 "WIA" 属性 "WIA \_ ip \_ 旋转"，提供驱动程序实现了此属性。 例如，假设在获取预览图像时，应用程序会将 WIA \_ ip \_ 旋转到 ROT180。 在这种情况下，传递给分段筛选器的图像的左上角实际上对应于平台的右下角。 因此，分段筛选器必须将它检测到的每个子区域的坐标映射到其平台上的坐标。 分段筛选器执行此映射后，可以将 WIA \_ ips \_ XPOS、wia \_ ip \_ YPOS 和其他属性值设置为与 subimage 相对应的子项。

请注意，在大多数情况下，WIA \_ ips \_ XPOS 和 wia \_ ip \_ YPOS 将设置为零，wia \_ IPS \_ 旋转将设置为纵向。 但是，分段应该能够处理它们未设置为这些值的情况。

另请注意，应用程序可以将映像传递到已由驱动程序旋转的分段筛选器，而不能传入已经执行了 deskewing 的映像。

 

