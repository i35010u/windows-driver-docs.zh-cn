---
title: 编译 NDIS 6.40 驱动程序
description: 本部分介绍如何编译 NDIS 6.40 驱动程序
ms.assetid: AF027939-06C7-435C-90D9-82272CED6A84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4d0cba0a654d8e9f6996f63e103ec601fcd0da0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555477"
---
# <a name="compiling-an-ndis-640-driver"></a>编译 6.40 NDIS 驱动程序


Windows 8.1 的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.40 驱动程序在编译时使用的合适的 NDIS 6.40 数据结构。

将以下编译器设置添加到您的驱动程序的 Visual Studio 项目：

-   微型端口驱动程序，将添加 NDIS640\_微型端口 = 1。

-   筛选器或协议驱动程序，将添加 NDIS640 = 1。

有关构建与 Windows 8.1 版本的 WDK 的驱动程序的信息，请参阅[构建一个驱动程序](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)。

有关将驱动程序的生成文件转换为 Visual Studio 项目的信息，请参阅[创建驱动程序从现有源文件](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_from_existing_source_files)。

 

 





