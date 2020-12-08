---
title: 链接到 NDIS 库
description: 链接到 NDIS 库
keywords:
- NDIS.sys WDK 网络
- NDIS 库 WDK 网络
- 链接 NDIS 库 WDK 网络
- 库 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4425ee626a64461431dfb51038d650e71e78a65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789697"
---
# <a name="linking-to-the-ndis-library"></a>链接到 NDIS 库





NDIS 库打包为 Ndis.sys，一种内核模式导出库，作为一组函数，重点介绍宏以获得最大性能。  (导出库是一个 .sys 文件，其工作方式类似于动态链接库。 ) 所有 NDIS 驱动程序将自身链接到 NDIS 库。 Microsoft Windows 驱动程序工具包 (WDK) 文档的网络参考部分介绍了 NDIS 库函数。

WDK 提供 Ndis .h 作为微型端口驱动程序的主头文件。 此文件定义微型端口驱动程序、NDIS 库函数和通用数据结构的入口点。 网络参考部分介绍了微型端口驱动程序、协议驱动程序和 **Ndis * Xxx*** 函数以及通用数据结构和 oid。

 

 





