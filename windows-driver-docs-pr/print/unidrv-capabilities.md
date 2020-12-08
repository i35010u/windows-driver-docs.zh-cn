---
title: Unidrv 功能
description: Unidrv 功能
keywords:
- Unidrv，功能
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcb9c64543e695a82f77906c4bf030b1726ecdbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808569"
---
# <a name="unidrv-capabilities"></a>Unidrv 功能





通用打印机驱动程序 (Unidrv) 提供以下功能：

-   支持所有非 Postscript 打印机，使用打印机特定的 [Unidrv 微型驱动程序](unidrv-minidrivers.md) 描述每个打印机的特征。

-   基于 TreeView 控件和属性表的 [Unidrv 用户界面](unidrv-user-interface.md)，对所有打印机都是一致的，但对于每个打印机的唯一选项也是可修改的。

-   单个 [Unidrv 呈现](unidrv-renderer.md) 器，与 GDI 图形引擎一起，将应用程序中的 MICROSOFT Win32 GDI 调用转换为可发送到打印后台处理程序的打印机命令。

 

 




