---
title: 应用程序项和驱动程序项
description: 应用程序项和驱动程序项
ms.assetid: 33b602dc-4a0b-47e1-90e2-b77ecc05f66d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17f2e83816dd4d51f1ad7cc6b3073942a8ef6e81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372606"
---
# <a name="application-items-and-driver-items"></a>应用程序项和驱动程序项





WIA 项表示设备属性和设备数据。 图像处理应用程序显示 WIA 设备为层次结构树的项，但根项，它表示在设备本身，以及任何表示图像或包含图像的文件夹的子项目。 应用程序发现时，树，但独立于创建和维护由 WIA 微型驱动程序的树。 当微型驱动程序创建的项的树时，WIA 服务将自动创建的图像处理应用程序即可查看此树的相同副本。 复制树中的项称为*应用程序项目*。 在树中创建的微型驱动程序的项目称为*驱动程序项*。

多个图像的应用程序可以在同一时间使用单一的图像处理设备。 因此，设备树中的项对象的每个应用程序的视图必须独立于另一个应用程序的视图。 实现这一点，如下所示：

1.  微型驱动程序创建的一个项树[IWiaDrvItem 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)对象使用[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)并[WIA 驱动程序服务库函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/index)。 此驱动程序项树中的项是微型驱动程序使用来表示设备的项的全局对象。

2.  当在树中的项图像处理应用程序请求访问时，WIA 服务将返回项对象的驱动程序项的副本。 当应用程序获取应用程序**IWiaItem** （Microsoft Windows SDK 文档中所述） 项对象 （应用程序项目），此对象与微型驱动程序的相应的 WIA 服务链接**IWiaDrvItem**中的对象*驱动程序项树*。

3.  WIA 创建一个单独*应用程序项树*对于每个应用程序，每个应用程序项树是驱动程序项树的副本。

应用程序通常使用**IWiaItem**对象来读取、 验证，并写入项属性，并请求项数据。

下图显示了应用程序项目与驱动程序项目的关系。

![说明应用程序项目和驱动程序项之间的关系的关系图](images/art-5.png)

如图所示，每个映像的应用程序具有其自己的项树的单独副本。 在应用程序项树的根项目包含返回到设备项树中的根项的指针。

本部分的其余部分包含以下主题：

[有关项的属性](about-item-properties.md)

[WIA 驱动程序项树](wia-driver-item-tree.md)

[WIA 照相机树](wia-camera-tree.md)

[WIA 扫描程序树](wia-scanner-tree.md)

[常用、 相机和扫描程序属性](common--camera--and-scanner-properties.md)

 

 




