---
title: 编译 NDIS 6.1 驱动程序
description: 本部分介绍如何编译 NDIS 6.1 驱动程序
keywords:
- NDIS WDK，编译标志
- 编译标志 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d50e5041cbfbd88ea1178abf0fed3d3ae61ce58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817609"
---
# <a name="compiling-an-ndis-61-driver"></a>编译 NDIS 6.1 驱动程序





Windows Server 2008 的生成实用工具支持标头版本控制。 标头版本控制可确保 NDIS 6.1 驱动程序在编译时使用合适的 NDIS 6.1 数据结构。 您必须更新源文件以指示 NDIS 6.1。

对于每种类型的驱动程序，将信息添加到源文件，如下所示：

-   对于微型端口驱动程序，请添加 NDIS61 \_ 微型端口 = 1。

-   对于协议驱动程序，请添加 NDIS61 = 1。

-   对于筛选器驱动程序，请添加 NDIS61 = 1。

 

 





