---
title: 筛选器初始化
description: 筛选器初始化
ms.assetid: c39dc5a6-f529-40a2-87d4-bac325b4fa1a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e6981da234bea64b79061dd685e7e512c695e9a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186899"
---
# <a name="filter-initialization"></a>筛选器初始化


崩溃转储驱动程序在系统崩溃或休眠进程的早期阶段进行初始化。 但是，一旦加载筛选器驱动程序，就会将其初始化。 这使筛选器驱动程序有机会在崩溃初始化时间（例如分配内存）期间执行任何必要的初始化。

在崩溃转储驱动程序堆栈中，筛选器驱动程序在系统启动时进行初始化。 你可以在系统运行时随时禁用和重新启用故障转储，因此崩溃转储筛选器驱动程序不应对驱动程序加载和卸载时间作出任何假设。 对于休眠，筛选器驱动程序会在启动休眠时加载并初始化。

将筛选器驱动程序加载到内存中后，崩溃转储驱动程序将调用筛选器驱动程序的 DriverEntry 函数来初始化筛选器驱动程序。 标准 DriverEntry 函数采用两个参数， (DriverObject 和 RegistryPath) 。 调用筛选器驱动程序时，DriverObject 将指向 [**筛选器 \_ 扩展**](/windows-hardware/drivers/ddi/ntdddump/ns-ntdddump-_filter_extension) 结构，RegistryPath 指向 [**筛选器 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/ntdddump/ns-ntdddump-_filter_initialization_data) 结构。

若要完成初始化过程，筛选器驱动程序应初始化 [**筛选器 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/ntdddump/ns-ntdddump-_filter_initialization_data) 结构，并将其返回到崩溃转储驱动程序。

 

