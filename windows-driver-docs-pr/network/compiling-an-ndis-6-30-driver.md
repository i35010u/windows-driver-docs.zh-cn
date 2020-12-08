---
title: 编译 NDIS 6.30 驱动程序
description: 本部分介绍如何编译 NDIS 6.30 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ef40c9a49c6a15775e8f20ec07b6c7f7cc90e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817607"
---
# <a name="compiling-an-ndis-630-driver"></a>编译 NDIS 6.30 驱动程序


在 windows 8 版本的 Windows 驱动程序工具包 (WDK) 中，驱动程序开发环境已集成到 Visual Studio 中。 Visual Studio 用户界面中提供了编码、构建、测试、调试、部署和发布驱动程序所需的大多数工具。 这是以前版本的 WDK 的出发，其中驱动程序生命周期的各个阶段都作为独立的任务使用独立的工具执行。

适用于 Windows 8 的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.30 驱动程序在编译时使用合适的 NDIS 6.30 数据结构。 将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

-   对于微型端口驱动程序，请添加 NDIS630 \_ 微型端口 = 1。

-   对于筛选器或协议驱动程序，请添加 NDIS630 = 1。

有关使用 Windows 8 版本的 WDK 构建驱动程序的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

有关将驱动程序的生成文件转换为 Visual Studio 项目的信息，请参阅 [从现有的源文件创建驱动程序](/windows-hardware/drivers)。

 

