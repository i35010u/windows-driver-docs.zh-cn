---
title: 编译 NDIS 6.1 驱动程序
description: 本部分介绍如何编译 NDIS 6.1 驱动程序
ms.assetid: 9606a91c-c1cb-4d93-b648-3829d1b51954
keywords:
- NDIS WDK 编译标志
- 编译标志 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7637120652f512ac2119a84036a09f3f0d3f5b14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534273"
---
# <a name="compiling-an-ndis-61-driver"></a>编译 6.1 NDIS 驱动程序





Windows Server 2008 的生成实用工具支持标头版本控制。 标头版本控制可确保 NDIS 6.1 驱动程序在编译时使用的合适的 NDIS 6.1 数据结构。 必须更新源文件以指示 NDIS 6.1。

对于每个类型的驱动程序，将信息添加到源文件，如下所示：

-   微型端口驱动程序，将添加 NDIS61\_微型端口 = 1。

-   协议驱动程序，将添加 NDIS61 = 1。

-   筛选器驱动程序，将添加 NDIS61 = 1。

 

 





