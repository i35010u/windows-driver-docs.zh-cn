---
title: 在驱动程序中使用注册表
description: 在驱动程序中使用注册表
ms.assetid: 69d2d491-3cc1-4fd0-a1c9-0cc8e73e69b2
keywords:
- 注册表 WDK 内核
- 驱动程序注册表信息 WDK 内核
- 存储 WDK 注册表
- 存储注册表信息
- 注册表 WDK 内核，有关驱动程序中的注册表
- 驱动程序注册表信息 WDK 内核，有关驱动程序中的注册表
- 操作注册表条目 WDK 内核
- WDK 内核注册表项
- 子项 WDK 内核注册表
- 内核模式驱动程序 WDK、 注册表
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 738699c9c45539aac64cd9b468c6826d6c78220b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372355"
---
# <a name="using-the-registry-in-a-driver"></a>在驱动程序中使用注册表





驱动程序，其他系统组件，如依赖于注册表中的存储配置信息。 系统本身使用注册表来存储有关设备和驱动程序的信息和驱动程序可以存储其他信息存在供自己使用。

Microsoft Windows 高级管理人员提供了用于操控注册表的例程的以下两个集：

[注册表项对象例程](registry-key-object-routines.md)

[注册表运行时库例程](registry-run-time-library-routines.md)

[Plug and Play 注册表例程](plug-and-play-registry-routines.md)

有关注册表的其他信息，请参阅：

[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[驱动程序的注册表项](https://msdn.microsoft.com/library/windows/hardware/ff549538)

 

 




