---
title: 支持初始化和终止函数
description: 支持初始化和终止函数
ms.assetid: 306be966-be23-4680-aeda-32e9cb1ac4a9
keywords:
- 绘制 WDK GDI 初始化
- 绘制 WDK GDI、 初始化、 有关
- 正在初始化图形驱动程序 WDK Windows 2000 显示
- 正在初始化图形驱动程序 WDK Windows 2000 显示大约
- GDI WDK Windows 2000 显示初始化
- GDI WDK Windows 2000 显示、 初始化、 有关
- 图形驱动程序 WDK Windows 2000 显示初始化
- 图形驱动程序 WDK Windows 2000 显示、 初始化、 有关
- GDI WDK Windows 2000 显示终止
- 图形驱动程序 WDK Windows 2000 显示终止
- 绘制 WDK GDI，终止
- 终止图形驱动程序 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e83a50a9f43bbd8ff8c659cbe3d7cbaa32dc8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377663"
---
# <a name="supporting-initialization-and-termination-functions"></a>支持初始化和终止函数


## <span id="ddk_supporting_initialization_and_termination_functions_gg"></span><span id="DDK_SUPPORTING_INITIALIZATION_AND_TERMINATION_FUNCTIONS_GG"></span>


图形驱动程序可以支持多个设备和多个并发的每个设备使用。 因此，初始化和终止发生在三个不同的层，每个层具有其自己计时。 初始化按以下顺序发生：

1.  [驱动程序初始化](driver-initialization-and-cleanup.md)

2.  [PDEV 初始化](pdev-initialization-and-cleanup.md)

3.  [图面上初始化](enabling-and-disabling-the-surface.md)

出现终止的情况相反的顺序。

 

 





