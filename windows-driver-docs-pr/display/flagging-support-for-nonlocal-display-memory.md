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
- 兼容性 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0627fe1770ac68bbf056193ec383e5de48c79e5a
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716040"
---
# <a name="flagging-support-for-nonlocal-display-memory"></a>非本地显示内存的标志支持


## <span id="ddk_flagging_support_for_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_NONLOCAL_DISPLAY_MEMORY_GG"></span>


驱动程序必须通知 DirectDraw (和 DirectDraw 应用程序) 它是 AGP 兼容的应用程序。 为此 \_ ，可以在[**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**DWCAPS2**成员中指定 DDCAPS2 NONLOCALVIDMEM，这是传递到 DirectDraw 的[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的一部分。

如果在不支持 AGP 服务的操作系统上运行，则 DirectDraw 将关闭 DDCAPS2 \_ NONLOCALVIDMEM 功能位和所有关联的非本地堆。

 

