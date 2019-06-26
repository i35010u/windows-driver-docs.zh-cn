---
title: 镜像中视频微型端口驱动程序 (XDDM) 驱动程序支持
description: 视频微型端口驱动程序中的镜像驱动程序支持（Windows 2000 模型）
ms.assetid: ca91e0a6-d619-432a-829e-49012951f27c
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，镜像驱动程序
- 镜像驱动程序 WDK Windows 2000 显示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 381680b4d007517a71a5bdfca2a4683c5c57e57a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382324"
---
# <a name="mirror-driver-support-in-video-miniport-drivers-windows-2000-model"></a>视频微型端口驱动程序中的镜像驱动程序支持（Windows 2000 模型）

*镜像驱动程序*支持的微型端口驱动程序提供由 Windows 2000 及更高版本，因此微型端口驱动程序必须没有任何特殊代码来尝试这种支持。 请参阅[镜像驱动程序](mirror-drivers.md)有关镜像系统中的显示器驱动程序详细信息。

镜像驱动程序微型端口驱动程序的要求是最低的。 它必须实现的唯一功能是对[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)，这由微型端口驱动程序及以下导出：

[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)

[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)

[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)

因为没有与镜像面关联的物理显示设备，所有这三个上述列表中所示的函数可以是始终返回成功的空实现。

**请注意**  从 Windows 8 开始，镜像驱动程序不会安装在系统上。 有关详细信息，请参阅[镜像驱动程序](mirror-drivers.md)。

 

 

 





