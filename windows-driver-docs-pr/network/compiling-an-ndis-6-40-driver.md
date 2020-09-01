---
title: 编译 NDIS 6.40 驱动程序
description: 本部分介绍如何编译 NDIS 6.40 驱动程序
ms.assetid: AF027939-06C7-435C-90D9-82272CED6A84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f910d61a99bd70a00320f825b66f3be5ab0d88f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208703"
---
# <a name="compiling-an-ndis-640-driver"></a>编译 NDIS 6.40 驱动程序


Windows 8.1 的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.40 驱动程序在编译时使用合适的 NDIS 6.40 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

-   对于微型端口驱动程序，请添加 NDIS640 \_ 微型端口 = 1。

-   对于筛选器或协议驱动程序，请添加 NDIS640 = 1。

有关使用 Windows 8.1 版本的 WDK 构建驱动程序的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

有关将驱动程序的生成文件转换为 Visual Studio 项目的信息，请参阅 [从现有的源文件创建驱动程序](/windows-hardware/drivers)。

 

