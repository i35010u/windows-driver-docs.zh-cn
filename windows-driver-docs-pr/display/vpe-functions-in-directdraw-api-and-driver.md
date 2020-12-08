---
title: DirectDraw API 和驱动程序中的 VPE 函数
description: DirectDraw API 和驱动程序中的 VPE 函数
keywords:
- DirectX VPE 支持 WDK DirectDraw，函数
- 绘制 VPEs WDK DirectDraw，函数
- DirectDraw VPEs WDK Windows 2000 显示，函数
- 视频端口扩展 WDK DirectDraw，函数
- VPEs WDK DirectDraw，函数
- 函数 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e5dc47632fde6278a9e51279d0797dd660846c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826587"
---
# <a name="vpe-functions-in-directdraw-api-and-driver"></a>DirectDraw API 和驱动程序中的 VPE 函数


## <span id="ddk_vpe_functions_in_directdraw_api_and_driver_gg"></span><span id="DDK_VPE_FUNCTIONS_IN_DIRECTDRAW_API_AND_DRIVER_GG"></span>


最新的 DirectX 版本中的视频端口扩展是 DirectDraw API 的低级扩展。 VPE 允许客户端（通常是 DirectShow）来协商 MPEG 或 NTSC 解码器与硬件视频端口之间的连接。 VPE 还允许客户端控制视频流中的效果，包括裁剪和缩放。

VPE 不是为应用程序广泛使用而设计的高级 API。 应用程序应使用 DirectShow，后者提供对 VPE 的免费支持。 下图显示了 VPE 和内核模式体系结构的简单视图。 有关详细信息，请参阅 [内核模式视频传输](kernel-mode-video-transport.md)。

![演示视频端口扩展和内核模式体系结构的示意图](images/ddfig10.png)

上图显示了 VPE 与 DirectDraw 体系结构的其他组件相关的情况。 DirectShow 使用 VPE 来协商连接，此连接提供有关如何传输数据和 V 同步和 H 同步信息的信息。 此信息可以是 (ITU 656) 的 APIC 连接、带有额外 pin 的外部数据行或专有数据流（例如由 Brooktree 和 Philips 实现的数据流）。

在连接协商中，VGA 硬件指示可支持哪些连接，MPEG 或 NTSC 解码器指示其首选项。 DirectShow 协商这两者之间的最佳连接。 连接被描述为 (GUID) 的全局唯一标识符，其中包含用于描述其他参数的标志，如双计时和活动视频。

 

 





