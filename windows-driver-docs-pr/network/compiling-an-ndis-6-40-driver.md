---
title: 编译 NDIS 6.40 驱动程序
description: 本部分介绍如何编译 NDIS 6.40 驱动程序
ms.assetid: AF027939-06C7-435C-90D9-82272CED6A84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f71f0a59b9f8961daea9eb38751f545736614f21
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815111"
---
# <a name="compiling-an-ndis-640-driver"></a>编译 NDIS 6.40 驱动程序


Windows 8.1 的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.40 驱动程序在编译时使用的合适的 NDIS 6.40 数据结构。

将以下编译器设置添加到您的驱动程序的 Visual Studio 项目：

-   微型端口驱动程序，将添加 NDIS640\_微型端口 = 1。

-   筛选器或协议驱动程序，将添加 NDIS640 = 1。

有关构建与 Windows 8.1 版本的 WDK 的驱动程序的信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

有关将驱动程序的生成文件转换为 Visual Studio 项目的信息，请参阅[创建驱动程序从现有源文件](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_from_existing_source_files)。

 

 





