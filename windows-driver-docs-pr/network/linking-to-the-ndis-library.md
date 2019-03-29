---
title: 链接到 NDIS 库
description: 链接到 NDIS 库
ms.assetid: eac33c9e-ff70-4a6c-b391-833a81faa079
keywords:
- NDIS.sys WDK 网络
- NDIS 库 WDK 网络
- 将 NDIS 库 WDK 网络链接
- 库 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0f8c87319aa9bb25b8428d3fe3349e63740b5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563341"
---
# <a name="linking-to-the-ndis-library"></a>链接到 NDIS 库





NDIS 库中 Ndis.sys，内核模式导出库打包为一组函数，注重最大性能的宏。 （导出库是一个.sys 文件，其功能类似的动态链接库。）所有的 NDIS 驱动程序自己链接到 NDIS 库。 Microsoft Windows Driver Kit (WDK) 文档中的网络参考各节所述的 NDIS 库函数。

WDK 提供 Ndis.h 作为主标头文件的微型端口驱动程序。 此文件定义微型端口驱动程序、 NDIS 库函数和通用数据结构的入口的点。 网络参考部分介绍的微型端口驱动程序、 协议驱动程序，并**Ndis * Xxx*** 函数的通用数据结构和 Oid。

 

 





