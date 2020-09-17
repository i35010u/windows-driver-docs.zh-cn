---
title: 用于内核模式视频传输的 DirectDraw 接口
description: 用于支持内核模式视频传输的 DirectDraw 接口
ms.assetid: 8012f6b0-3b55-438f-8146-4f62e6bafad3
keywords:
- 内核模式视频传输 WDK DirectDraw，接口
- DirectX VPE 支持 WDK DirectDraw、内核模式视频传输
- 绘制 VPEs WDK DirectDraw，内核模式视频传输
- DirectDraw VPEs WDK Windows 2000 显示器、内核模式视频传输
- 视频端口扩展 WDK DirectDraw、内核模式视频传输
- VPEs WDK DirectDraw，内核模式视频传输
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 76e0548a2d882a15092ec61f2e7d56343c0c73d2
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715474"
---
# <a name="directdraw-interfaces-for-kernel-mode-video-transport-support"></a>用于支持内核模式视频传输的 DirectDraw 接口

内核模式视频传输必须跟踪它使用的每个表面的图面信息，以及每个 VPE 对象的信息。 每次为 surface 或硬件视频端口调用 [*DdUpdateOverlay*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay) 或 [*DdVideoPortUpdate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_vportcb_update) 时，都必须更新该信息。 在 DirectDraw 将此信息发送到内核模式视频传输之前，它将调用以下两个驱动程序函数之一： [*DdSyncSurfaceData*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface) 或 [*DdSyncVideoPortData*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)。 使用这些函数，驱动程序可以填充或修改部分结构信息，并使用 dd [** \_ SYNCSURFACEDATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_syncsurfacedata)的四个**dwDriverReserved**_n_个成员或[**dd \_ SYNCVIDEOPORTDATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_syncvideoportdata)结构的三个**dwDriverReserved**_n_个成员来实现自己的目的。 这些驱动程序函数是内核模式视频传输支持正常工作所必需的。

有关驱动程序如何使用这些 **dwDriverReserved**_N_ 成员的一个很好的示例是设置一个标志，该标志指示覆盖面在硬件支持多个物理覆盖的情况。

 

