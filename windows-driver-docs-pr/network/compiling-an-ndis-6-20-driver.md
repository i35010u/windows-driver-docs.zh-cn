---
title: 编译 NDIS 6.20 驱动程序
description: 本部分介绍如何编译 NDIS 6.20 驱动程序
ms.assetid: 07940d98-63fb-4629-943c-f56ebdfcdd76
keywords:
- NDIS 6.20 WDK，编译了驱动程序
- 编译的 NDIS 6.20 驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb684ca05c4320688ad21317a87460de6b5c4458
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343665"
---
# <a name="compiling-an-ndis-620-driver"></a>编译 NDIS 6.20 驱动程序





生成实用工具适用于 Windows 7 及更高版本支持标头版本控制。 标头版本控制可确保 NDIS 6.20 驱动程序在编译时使用的合适的 NDIS 6.20 数据结构。 必须更新以指示 NDIS 6.20 的源文件。

对于每个类型的驱动程序，将信息添加到源文件，如下所示：

-   微型端口驱动程序，将添加 NDIS620\_微型端口 = 1。

-   协议驱动程序，将添加 NDIS620 = 1。

-   筛选器驱动程序，将添加 NDIS620 = 1。

 

 





