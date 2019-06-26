---
title: 分段筛选器的实现说明
description: 分段筛选器的实现说明
ms.assetid: c4caf8dd-8108-4bc7-b02f-1e180fedb95f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b0c34623612289bcbd9f0c5b075a99ff6c24628
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373529"
---
# <a name="implementation-notes-for-segmentation-filters"></a>分段筛选器的实现说明





请务必注意分段筛选器设置到它将创建每个子项的属性。 这些属性包括：[**WIA\_IPS\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)， [ **WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)， [ **WIA\_IPS\_大 XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)，WIA\_IP\_YEXTENT，并可能[ **WIA\_IP\_反扭曲\_X** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-x)并[ **WIA\_IP\_反扭曲\_Y**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-y)。 这些属性值对应于在平台中，不传递到映像中的项的位置*pInputStream*参数。

因此，很重要分段筛选器密切注意 WIA\_IPS\_XPOS、 WIA\_IP\_YPOS，和[ **WIA\_IP\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation)传入的映像的属性。

例如，假设应用程序执行一次预览扫描它在其中设置 WIA\_IPS\_XPOS = WIA\_IP\_YPOS 才会获取预览图像 （父） 项到 = 200。 然后它调用到分段筛选器以检测可能的子区域。 但是，在分段筛选器中使用的实际算法作用于传递给它的映像。 如果此算法检测到图像的左边的缘和 200 像素，向下的右角 150 像素的子区域到从图像的顶部，这实际上对应于位于一个点 （350，400） 上扫描程序。

在下图中，外部的区域表示的扫描程序平板。 尽管该算法将查找区域的左上角的坐标为 （150，200） 值的分段的筛选器应设置到子项目 WIA\_IP\_XPOS 和 WIA\_IP\_YPOS 为 350 和 400。

![说明分段筛选器应用于的辊部分的关系图](images/art-segmentation3.png)

例如，应用程序将显示以可视方式分段筛选器检测到的区域，如果它必须了解分段筛选器设置到平台中的位置相对应的坐标。 这意味着应用程序必须将平板坐标映射到的预览图像中的坐标。 在大多数情况下，但是，应用程序将执行预览扫描使用 WIA\_IPS\_XPOS = WIA\_IPS\_YPOS = 0 且没有旋转 ([**WIA\_IP\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation) = 纵向)。 如果是这样，则在平台的坐标和中的预览图像之间的直接映射。

分段的筛选器必须特别注意的另一个属性是旋转属性，WIA\_IP\_旋转，提供该驱动程序实现此属性。 例如假定时获取的预览图像，应用程序设置 WIA\_IP\_ROT180 的旋转。 在这种情况下传递到分段的筛选器的图像的左上角实际上对应于在平台的右下角。 因此，分段的筛选器必须映射到其坐标在平台应为旋转的图像中检测到它的每个子区域的坐标。 一旦分段筛选器执行了此映射，它可以设置 WIA\_IPS\_XPOS、 WIA\_IP\_YPOS 和其他属性值到子项目与 subimage 相对应。

注意，在大多数情况下，WIA\_IPS\_XPOS 和 WIA\_IPS\_YPOS 将设置为零，并且 WIA\_IP\_旋转将设置为纵向。 但是，分段应能处理种情况下在其中它们未设置这些值。

另请注意，虽然应用程序可以在图像中传递给驱动程序已旋转分段筛选器，它必须不通过在其噪已经执行了图像中。

 

 




