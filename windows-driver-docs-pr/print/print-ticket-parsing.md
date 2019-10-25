---
title: 打印票证分析
description: 打印票证分析
ms.assetid: 8328110a-abb4-47aa-ab1d-730e4a2ce7bd
keywords:
- XPSDrv 打印机驱动程序 WDK，呈现模块
- 渲染模块 WDK XPSDrv，打印票证
- 打印票证 WDK，XPSDrv 打印机驱动程序
- 分析打印票证对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5071e3cd20b2ee6585297ae7e68f2cd2d894401b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842339"
---
# <a name="print-ticket-parsing"></a>打印票证分析


为当前文档部件合并打印票证后，打印驱动程序筛选器必须分析内容以查找应用于筛选器的设置。 [IPrintCoreHelper 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)的方法可用于打印驱动程序筛选器模块，以帮助分析打印票证元素。 从打印票证中提取了打印票证元素后，可以将其集成到筛选器模块函数中。 " [XPS 筛选器管道](xpsdrv-printer-driver.md)" 部分介绍了筛选器模块。

 

 




