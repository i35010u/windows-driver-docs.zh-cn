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
ms.openlocfilehash: 703610e1fc7d4a74d7134a9ffe1420a93f7cebd1
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065448"
---
# <a name="flagging-support-for-nonlocal-display-memory"></a>非本地显示内存的标志支持


## <span id="ddk_flagging_support_for_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_NONLOCAL_DISPLAY_MEMORY_GG"></span>


驱动程序必须通知 DirectDraw (和 DirectDraw 应用程序) 它是 AGP 兼容的应用程序。 为此 \_ ，可以在[**DDCORECAPS**](/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**DWCAPS2**成员中指定 DDCAPS2 NONLOCALVIDMEM，这是传递到 DirectDraw 的[**DD \_ HALINFO**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的一部分。

如果在不支持 AGP 服务的操作系统上运行，则 DirectDraw 将关闭 DDCAPS2 \_ NONLOCALVIDMEM 功能位和所有关联的非本地堆。

 

