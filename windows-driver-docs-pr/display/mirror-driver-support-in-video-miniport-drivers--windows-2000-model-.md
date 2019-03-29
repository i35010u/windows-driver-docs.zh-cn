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
ms.openlocfilehash: a14f99bcd3e360fe494f27ff2264b3c67d1d205a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566551"
---
# <a name="mirror-driver-support-in-video-miniport-drivers-windows-2000-model"></a>视频微型端口驱动程序中的镜像驱动程序支持（Windows 2000 模型）

*镜像驱动程序*支持的微型端口驱动程序提供由 Windows 2000 及更高版本，因此微型端口驱动程序必须没有任何特殊代码来尝试这种支持。 请参阅[镜像驱动程序](mirror-drivers.md)有关镜像系统中的显示器驱动程序详细信息。

镜像驱动程序微型端口驱动程序的要求是最低的。 它必须实现的唯一功能是对[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556159)，这由微型端口驱动程序及以下导出：

[*HwVidFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff567332)

[*HwVidInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff567345)

[*HwVidStartIO*](https://msdn.microsoft.com/library/windows/hardware/ff567367)

因为没有与镜像面关联的物理显示设备，所有这三个上述列表中所示的函数可以是始终返回成功的空实现。

**请注意**  从 Windows 8 开始，镜像驱动程序不会安装在系统上。 有关详细信息，请参阅[镜像驱动程序](mirror-drivers.md)。

 

 

 





