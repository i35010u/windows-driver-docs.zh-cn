---
title: 在基于 x86 的计算机中的开窗 Vdm
description: 在基于 x86 的计算机中的开窗 Vdm
ms.assetid: 01250cef-1ddb-4b32-a155-0170e1e4517a
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，VGA，在基于 x86 的计算机中的开窗 Vdm
- VGA WDK 视频微型端口，在基于 x86 的计算机中的开窗 Vdm
- 在基于 x86 的计算机 WDK 视频微型端口的开窗 Vdm
- 基于 x86 的计算机兼容的 VGA WDK 的微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49eaf87deb795ba00cc6052d2e99169cb1a19998
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542366"
---
# <a name="windowed-vdms-in-x86-based-machines"></a>在基于 x86 的计算机中的开窗 Vdm


## <span id="ddk_windowed_vdms_in_x86_based_machines_gg"></span><span id="DDK_WINDOWED_VDMS_IN_X86_BASED_MACHINES_GG"></span>


每个 MS-DOS 应用程序作为 Windows 运行*VDM*，后者又，作为在 Win32 中的控制台管理器应用程序运行受保护的子系统。

在基于 NT 的操作系统平台调用内核模式组件*V86 模拟器*捕获 I/O 颁发的 MS-DOS 应用程序的说明进行操作。 只要一时段内运行此类应用程序，其尝试访问视频适配器的端口是捕获并反映回系统提供视频*VDD*，这模拟的应用程序适配器的行为。

换而言之，显示器驱动程序保留的视频适配器的控件 VDM 在窗口中运行时。

 

 





