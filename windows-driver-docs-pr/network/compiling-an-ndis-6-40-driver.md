---
title: 编译 NDIS 6.40 驱动程序
description: 本部分介绍如何编译 NDIS 6.40 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60a4be8b4d71cea486eda7e9ff6f3f31be245f13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817151"
---
# <a name="compiling-an-ndis-640-driver"></a>编译 NDIS 6.40 驱动程序


Windows 8.1 的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.40 驱动程序在编译时使用合适的 NDIS 6.40 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

-   对于微型端口驱动程序，请添加 NDIS640 \_ 微型端口 = 1。

-   对于筛选器或协议驱动程序，请添加 NDIS640 = 1。

有关使用 Windows 8.1 版本的 WDK 构建驱动程序的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

有关将驱动程序的生成文件转换为 Visual Studio 项目的信息，请参阅 [从现有的源文件创建驱动程序](/windows-hardware/drivers)。

 

