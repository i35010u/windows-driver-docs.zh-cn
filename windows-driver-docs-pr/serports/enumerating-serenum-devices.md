---
title: 枚举 Serenum 设备
description: 枚举 Serenum 设备
keywords:
- Serenum 驱动程序 WDK，设备枚举
- 枚举 Serenum 设备 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f6fcfb727c5e42d08ae3bee91c3bc1343d43429
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805037"
---
# <a name="enumerating-serenum-devices"></a>枚举 Serenum 设备





在 Microsoft Windows 2000 中，启动时间会大幅延迟，自动枚举高容量的多端口适配器 (包含16个或更多端口) 。 为了解决此问题，Windows XP 和更高版本支持以下增强功能：

-   与 Windows 2000 相比，Serenum 要求自动枚举高容量的多端口适配器的时间已大大降低。

-   在 Windows XP 及更高版本中，对于系统上安装的每个串行端口，Serenum 支持可选的 **SkipEnumerations** 注册表项值。 供应商可以使用此输入值来控制 Serenum 是否枚举端口 (由系统启动或用户通过设备管理器或添加硬件向导) 启动。

有关如何在 Windows XP 中设置串行端口的 **SkipEnumerations** 入口值的详细信息，请参阅 [Serenum 的注册表设置](registry-settings-for-serenum.md)。

Windows 不支持单个注册表设置，全局控制所有串行端口的枚举。

Serenum 必须打开串行端口才能枚举它。 使端口保持打开状态的设备不应使用 Serenum。

 

 




