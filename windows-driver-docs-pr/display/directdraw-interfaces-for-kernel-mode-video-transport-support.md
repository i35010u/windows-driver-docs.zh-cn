---
title: 内核模式视频传输的 DirectDraw 接口
description: 用于支持内核模式视频传输的 DirectDraw 接口
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
ms.openlocfilehash: 051e453ba8d2e58ef05d1ec64746693978b22819
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716867"
---
# <a name="directdraw-interfaces-for-kernel-mode-video-transport-support"></a>用于支持内核模式视频传输的 DirectDraw 接口

内核模式视频传输必须跟踪的使用，每个面的和每个 VPE 对象图面上的信息。 此信息必须更新每次都[ *DdUpdateOverlay* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay)或[ *DdVideoPortUpdate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update)称为面或硬件视频端口。 DirectDraw 将此信息发送到内核模式视频传输之前，它将调用两个驱动程序函数之一：[*DdSyncSurfaceData* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface)或[ *DdSyncVideoPortData*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)。 这些函数允许驱动程序填充或修改某些结构信息以及使用四**dwDriverReserved**_N_的成员[ **DD\_SYNCSURFACEDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_syncsurfacedata)或三个**dwDriverReserved**_N_的成员[ **DD\_SYNCVIDEOPORTDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_syncvideoportdata)其自身的用途的结构。 这些驱动程序函数所需的内核模式视频传输支持才能正常工作。

很好的驱动程序可以使用这些示例**dwDriverReserved**_N_成员是设置一个标志，指示哪个物理覆盖覆盖面使用如果硬件支持多个物理覆盖。

 

 





