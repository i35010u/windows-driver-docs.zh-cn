---
title: 报告非本地显示内存的 DDraw 功能
description: DMA 模型驱动程序对非本地显示内存的功能与本地显示内存的功能不同。
ms.assetid: e503fc8b-db27-486a-8616-a1b88ea77218
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw，DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw，DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw，DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP、DMA 样式 AGP
- 报告 DirectDraw 功能
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 77807a1207563539137ea966329cda23f4349968
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064626"
---
# <a name="reporting-directdraw-capabilities-for-nonlocal-display-memory"></a>报告非本地显示内存的 DirectDraw 功能

DMA 模型驱动程序对非本地显示内存的功能与本地显示内存的功能不同。 例如，显示卡可能能够拉伸 array.blit 本地显示内存表面，但不能拉伸非本地显示内存图面。 如果驱动程序指定 DDCAPS2 \_ NONLOCALVIDMEMCAPS 标志，则会通过 [**DdGetDriverInfo**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 驱动程序入口点探测驱动程序的非本地显示内存表面的 DirectDraw 功能。 标识此探测的 GUID 是 GUID \_ NonLocalVidMemCaps。

请务必注意，对于此版本的 DirectDraw，驱动程序只能指定从非本地显示内存到本地显示内存的 blts 功能。 从本地显示内存传输到非本地显示内存，以及从非本地显示内存传输到非本地显示内存，由 DirectDraw HEL 始终进行模拟。 将来的版本中可能会放宽此限制。

 

