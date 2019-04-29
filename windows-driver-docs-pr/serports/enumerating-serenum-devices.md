---
title: 枚举 Serenum 设备
description: 枚举 Serenum 设备
ms.assetid: c850c52b-82d7-48c2-a6c4-bfd071756632
keywords:
- Serenum 驱动程序 WDK，设备枚举
- 枚举 Serenum 设备 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db8c6cf08bc875c2f096b0d1c3b5156b1caaf8d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370984"
---
# <a name="enumerating-serenum-devices"></a>枚举 Serenum 设备





在 Microsoft Windows 2000 中，启动时可能会显著延迟自动枚举 （包含 16 个或多个端口） 的高容量多端口适配器所需的时间。 若要解决此问题，Windows XP 和更高版本支持以下增强功能：

-   与 Windows 2000 相比，会大大减少 Serenum 自动枚举高容量多端口适配器所需的时间。

-   在 Windows XP 及更高版本，支持的可选 Serenum **SkipEnumerations**系统上安装的每个串行端口的注册表条目值。 一个供应商可以使用此项值来控制是否 Serenum 枚举一个端口 （无论是通过系统启动或用户通过设备管理器或添加硬件向导启动）。

有关如何设置串行端口的详细信息**SkipEnumerations**条目值，在 Windows XP 中，请参阅[Serenum 的注册表设置](registry-settings-for-serenum.md)。

Windows 不支持全局控制所有串行端口的枚举的单个注册表设置。

Serenum 必须打开用于其进行枚举的串行端口。 无限期地保留一个端口打开的设备不应使用 Serenum。

 

 




