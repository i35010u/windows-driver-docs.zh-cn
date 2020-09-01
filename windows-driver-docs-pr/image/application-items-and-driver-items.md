---
title: 应用程序项和驱动程序项
description: 应用程序项和驱动程序项
ms.assetid: 33b602dc-4a0b-47e1-90e2-b77ecc05f66d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2ebdd07cf11971a0e79dd6fd7ca668b19a01c01
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189893"
---
# <a name="application-items-and-driver-items"></a>应用程序项和驱动程序项





WIA 项表示设备属性和设备数据。 图像处理应用程序将 WIA 设备视为项的层次结构树，根项表示设备本身，子项表示包含图像的图像或文件夹。 但是，应用程序看到的树与由 WIA 微型驱动程序创建和维护的树分开。 当微型驱动程序创建项目树时，WIA 服务会自动创建此树的相同副本，该副本可由图像应用程序查看。 复制树中的项称为 *应用程序项*。 微型驱动程序创建的树中的项称为 " *驱动程序项*"。

多个映像应用程序可以同时使用单个图像设备。 因此，设备树中项对象的每个应用程序的视图必须独立于另一个应用程序的视图。 这通过以下操作实现：

1.  微型驱动程序使用[IWiaMiniDrv 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)和[WIA 驱动程序服务库函数](/windows-hardware/drivers/ddi/wiamdef/index)创建[IWiaDrvItem 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)对象的项树。 此驱动程序项树中的项是全局对象，微型驱动程序使用它们来表示设备的项。

2.  当映像应用程序请求访问树中的某一项时，WIA 服务将返回一个项对象，该对象是驱动程序项的副本。 当应用程序获取应用程序**IWiaItem** (Microsoft Windows SDK 文档) item 对象 (应用程序) 项中所述）时，WIA 服务会将此对象链接到*驱动程序项树*中微型驱动程序的相应**IWiaDrvItem**对象。

3.  WIA 为每个应用程序创建一个单独的 *应用程序项树* ，每个应用程序项树都是驱动程序项树的副本。

应用程序通常使用 **IWiaItem** 对象来读取、验证和写入项属性，并请求项数据。

下图显示了应用程序项与驱动程序项之间的关系。

![说明应用程序项和驱动程序项之间的关系的关系图](images/art-5.png)

如图所示，每个图像应用程序都有自己的项树的单独副本。 应用程序项树中的根项包含一个指针，该指针返回到设备项树中的根项。

本部分的其余部分包含以下主题：

[关于项属性](about-item-properties.md)

[WIA 驱动程序项树](wia-driver-item-tree.md)

[WIA 相机树](wia-camera-tree.md)

[WIA 扫描仪树](wia-scanner-tree.md)

[常用属性、相机属性和扫描仪属性](common--camera--and-scanner-properties.md)

 

