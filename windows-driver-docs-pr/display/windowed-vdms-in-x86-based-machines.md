---
title: 基于 x86 的计算机中的开窗 VDM
description: 基于 x86 的计算机中的开窗 VDM
keywords:
- 基于 x86 的计算机中的视频微型端口驱动程序 WDK Windows 2000、VGA、开窗 VDMs
- 基于 x86 的计算机中的 VGA WDK 视频微型端口，开窗 VDMs
- 基于 x86 的计算机中的开窗 VDMs WDK 视频微型端口
- 基于 x86 的计算机 WDK VGA 兼容视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5aca325f12d2502e3d6758fa89ad7fe23f4bf95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826015"
---
# <a name="windowed-vdms-in-x86-based-machines"></a>基于 x86 的计算机中的开窗 VDM


## <span id="ddk_windowed_vdms_in_x86_based_machines_gg"></span><span id="DDK_WINDOWED_VDMS_IN_X86_BASED_MACHINES_GG"></span>


每个 MS-DOS 应用程序都作为一个 Windows *VDM* 运行，后者又作为受保护的子系统中的控制台管理器应用程序运行。

在基于 NT 的操作系统平台中，称为 *V86 模拟器* 的内核模式组件捕获由 MS-DOS 应用程序发出的 i/o 说明。 只要此类应用程序在窗口中运行，就会捕获其访问视频适配器端口的尝试并反映到系统提供的视频 *VDD* 中，这将模拟应用程序的适配器的行为。

换句话说，当 VDM 在窗口中运行时，显示驱动程序将保留对视频适配器的控制。

 

 





