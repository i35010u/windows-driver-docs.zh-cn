---
title: 打印票证分析
description: 打印票证分析
ms.assetid: 8328110a-abb4-47aa-ab1d-730e4a2ce7bd
keywords:
- XPSDrv 的打印机驱动程序 WDK，呈现模块
- 呈现模块 WDK XPSDrv 打印票证
- 打印票证 WDK，XPSDrv 的打印机驱动程序
- 分析的打印票证对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0d061497ef14d0589dc76db55bfd98f887995b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351890"
---
# <a name="print-ticket-parsing"></a>打印票证分析


打印票证已合并为当前的文档部件后，打印驱动程序筛选器必须分析内容，以查找应用于筛选器的设置。 方法[IPrintCoreHelper 接口](https://msdn.microsoft.com/library/windows/hardware/ff552960)可以打印驱动程序筛选器模块中用于帮助分析的打印票证元素。 从打印票证中提取了打印票证元素后，他们可以集成到筛选器模块函数。 筛选器模块中所述[XPS 筛选器管道](xpsdrv-printer-driver.md)部分。

 

 




