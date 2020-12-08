---
title: 支持初始化和终止函数
description: 支持初始化和终止函数
keywords:
- 绘制 WDK GDI，初始化
- 绘制 WDK GDI，初始化，关于
- 初始化图形驱动程序 WDK Windows 2000 显示
- 初始化图形驱动程序 WDK Windows 2000 显示，关于
- GDI WDK Windows 2000 显示，初始化
- GDI WDK Windows 2000 显示，初始化，关于
- 图形驱动程序 WDK Windows 2000 显示，初始化
- 图形驱动程序 WDK Windows 2000 显示、初始化、关于
- GDI WDK Windows 2000 显示、终止
- 图形驱动程序 WDK Windows 2000 显示、终止
- 绘制 WDK GDI，终止
- 终止图形驱动程序 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f390dbba01191c4195d1f84e56f7f8b594a8689e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793849"
---
# <a name="supporting-initialization-and-termination-functions"></a>支持初始化和终止函数


## <span id="ddk_supporting_initialization_and_termination_functions_gg"></span><span id="DDK_SUPPORTING_INITIALIZATION_AND_TERMINATION_FUNCTIONS_GG"></span>


图形驱动程序可以支持多个设备，并可多次使用每个设备。 因此，初始化和终止发生在三个不同的层中，每个层都有自己的计时。 初始化按以下顺序发生：

1.  [驱动程序初始化](driver-initialization-and-cleanup.md)

2.  [PDEV 初始化](pdev-initialization-and-cleanup.md)

3.  [图面初始化](enabling-and-disabling-the-surface.md)

终止发生顺序相反。

 

 





