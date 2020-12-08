---
title: 编译 NDIS 6.20 驱动程序
description: 本部分介绍如何编译 NDIS 6.20 驱动程序
keywords:
- NDIS 6.20 WDK，编译驱动程序
- 编译 NDIS 6.20 驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 210527c03f4dadfe1b030792b4471505ca5b4413
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782285"
---
# <a name="compiling-an-ndis-620-driver"></a>编译 NDIS 6.20 驱动程序





适用于 Windows 7 和更高版本的生成实用工具支持标头版本控制。 标头版本控制可确保 NDIS 6.20 驱动程序在编译时使用合适的 NDIS 6.20 数据结构。 您必须更新源文件以指示 NDIS 6.20。

对于每种类型的驱动程序，将信息添加到源文件，如下所示：

-   对于微型端口驱动程序，请添加 NDIS620 \_ 微型端口 = 1。

-   对于协议驱动程序，请添加 NDIS620 = 1。

-   对于筛选器驱动程序，请添加 NDIS620 = 1。

 

 





