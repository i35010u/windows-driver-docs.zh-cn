---
title: DirectDraw API 和驱动程序中的 VPE 函数
description: DirectDraw API 和驱动程序中的 VPE 函数
ms.assetid: 7e899f20-4082-4438-b7f2-198d1a4ad344
keywords:
- DirectX VPE 支持 WDK DirectDraw，函数
- 绘制 VPEs WDK DirectDraw，函数
- DirectDraw VPEs WDK Windows 2000 显示中函数
- 视频端口扩展 WDK DirectDraw，函数
- VPEs WDK DirectDraw 函数
- WDK 的视频端口扩展函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0963f17d65818f236dcb1ad3708ccad39e1946d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544974"
---
# <a name="vpe-functions-in-directdraw-api-and-driver"></a>DirectDraw API 和驱动程序中的 VPE 函数


## <span id="ddk_vpe_functions_in_directdraw_api_and_driver_gg"></span><span id="DDK_VPE_FUNCTIONS_IN_DIRECTDRAW_API_AND_DRIVER_GG"></span>


最新的 DirectX 版本中的视频端口扩展是低级别 DirectDraw API 扩展。 VPE 允许客户端-通常 DirectShow-协商 MPEG 或 NTSC 解码器与硬件之间的连接的视频端口。 VPE 还允许客户端到控件中的视频流，包括剪切和缩放效果。

VPE 不能广泛用于应用程序的高级别 API。 应用程序应使用 DirectShow，提供对 VPE 的免费支持。 下图显示了 VPE 和内核模式的体系结构的简单视图。 有关详细信息，请参阅[内核模式视频传输](kernel-mode-video-transport.md)。

![关系图演示的视频端口扩展和内核模式体系结构](images/ddfig10.png)

上图显示 VPE 了相对于 DirectDraw 体系结构的其他组件。 DirectShow 使用 VPE 协商连接，它提供了有关如何传输数据和 V 同步和 H 同步信息的信息。 此信息可以是一个 APIC 连接 (ITU 656)、 具有额外的 pin 或专有的数据流，例如那些由 Brooktree 和 Philips 实现的外部数据行。

在连接的协商，VGA 硬件指示可以支持哪些连接，并由 MPEG 或 NTSC 解码器指示其首选项。 DirectShow 协商两者之间的最佳连接。 使用标志来描述其他参数，例如双精度的计时和视频活动描述作为全局唯一标识符 (GUID) 的连接。

 

 





