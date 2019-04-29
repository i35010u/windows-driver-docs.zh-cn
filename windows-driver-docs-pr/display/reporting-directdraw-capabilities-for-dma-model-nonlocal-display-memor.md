---
title: 对于非本地显示内存报告 ddraw 会功能
description: DMA 模型驱动程序包含适用于本地显示内存的非本地显示内存比不同的功能。
ms.assetid: e503fc8b-db27-486a-8616-a1b88ea77218
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP DMA 样式 AGP
- DirectDraw 的报告功能
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 92475ad722fdf15ade9ae5c8fd09382db2f5ecf7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383275"
---
# <a name="reporting-directdraw-capabilities-for-nonlocal-display-memory"></a>报告非本地显示内存的 DirectDraw 功能

DMA 模型驱动程序包含适用于本地显示内存的非本地显示内存比不同的功能。 例如，显示卡可能能够拉伸位块本地显示内存图面，但显示不非本地内存图面。 如果该驱动程序指定 DDCAPS2\_NONLOCALVIDMEMCAPS 标志，该驱动程序会探测的非本地显示内存的 DirectDraw 功能通过 surface [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)驱动程序入口点。 标识此探测的 GUID 是 GUID\_NonLocalVidMemCaps。

请务必注意，对于此版本，它的 DirectDraw，驱动程序可以仅指定功能的 blts 从非本地显示内存本地显示内存。 DirectDraw HEL 始终模拟从非本地显示内存和本地显示内存和非本地显示内存与非本地显示内存传输。 未来版本中可能会放宽此限制。

 

 





