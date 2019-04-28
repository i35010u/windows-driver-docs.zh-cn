---
title: 非本地显示内存的标志支持
description: 非本地显示内存的标志支持
ms.assetid: 5e5187e8-ff93-48e0-997d-71d65d35757f
keywords:
- 显示内存 WDK DirectDraw，兼容性
- 非本地显示内存 WDK DirectDraw，兼容性
- AGP WDK DirectDraw，兼容性
- 绘制 AGP 支持 WDK DirectDraw，兼容性
- DirectDraw AGP 支持 WDK Windows 2000 显示，兼容性
- 内存 WDK DirectDraw AGP，兼容性
- WDK DirectDraw 的兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88fb1aa3c5a2faaa092392b2b70f5dc92b491627
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347579"
---
# <a name="flagging-support-for-nonlocal-display-memory"></a>非本地显示内存的标志支持


## <span id="ddk_flagging_support_for_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_NONLOCAL_DISPLAY_MEMORY_GG"></span>


驱动程序必须通知 DirectDraw （和 DirectDraw 应用程序），它是的 AGP 兼容。 这可以通过指定功能位 DDCAPS2\_中的 NONLOCALVIDMEM **dwCaps2**的成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)结构，它是一部分[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构传递给 DirectDraw。

如果不支持 AGP 服务的操作系统上运行，DirectDraw 关闭 DDCAPS2\_NONLOCALVIDMEM 功能位以及所有关联的非本地堆。

 

 





