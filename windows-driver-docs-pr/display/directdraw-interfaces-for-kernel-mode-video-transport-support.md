---
title: 内核模式视频传输的 DirectDraw 接口
description: 内核模式视频传输支持的 DirectDraw 接口
ms.assetid: 8012f6b0-3b55-438f-8146-4f62e6bafad3
keywords:
- 内核模式视频传输 WDK DirectDraw 接口
- DirectX VPE 支持 WDK DirectDraw 内核模式视频传输
- 绘制 VPEs WDK DirectDraw，内核模式视频传输
- DirectDraw VPEs WDK Windows 2000 显示，内核模式视频传输
- 视频端口扩展 WDK DirectDraw，内核模式视频传输
- VPEs WDK DirectDraw，内核模式视频传输
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 27f058bd394289246e0cd937711cbdf325b1ed2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542236"
---
# <a name="directdraw-interfaces-for-kernel-mode-video-transport-support"></a>内核模式视频传输支持的 DirectDraw 接口

内核模式视频传输必须跟踪的使用，每个面的和每个 VPE 对象图面上的信息。 此信息必须更新每次都[ *DdUpdateOverlay* ](https://msdn.microsoft.com/library/windows/hardware/ff550369)或[ *DdVideoPortUpdate* ](https://msdn.microsoft.com/library/windows/hardware/ff550450)称为面或硬件视频端口。 DirectDraw 将此信息发送到内核模式视频传输之前，它将调用两个驱动程序函数之一：[*DdSyncSurfaceData* ](https://msdn.microsoft.com/library/windows/hardware/ff550345)或[ *DdSyncVideoPortData*](https://msdn.microsoft.com/library/windows/hardware/ff550350)。 这些函数允许驱动程序填充或修改某些结构信息以及使用四个 **dwDriverReserved * * * N*的成员[ **DD\_SYNCSURFACEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551739)或三个 **dwDriverReserved * * * N*的成员[ **DD\_SYNCVIDEOPORTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551740)其自身的用途的结构。 这些驱动程序函数所需的内核模式视频传输支持才能正常工作。

很好的驱动程序可以使用这些示例 **dwDriverReserved * * * N*成员是设置一个标志，指示哪个物理覆盖覆盖面使用如果硬件支持多个物理覆盖。

 

 





