---
title: 磁带驱动程序简介
description: 磁带驱动程序
keywords:
- 磁带驱动程序 WDK 存储
- 存储磁带驱动程序 WDK
- 存储驱动程序 WDK，磁带驱动程序
- 磁带驱动程序 WDK 存储，关于磁带驱动程序
- 存储磁带驱动程序 WDK，关于磁带驱动程序
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: d7d4a9a0a59861b8de876741831549ff0ad7fe74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834905"
---
# <a name="introduction-to-tape-drivers"></a>磁带驱动程序简介

基于 NT 的操作系统提供了通用的磁带类驱动程序，用于处理特定于操作系统和与设备无关的磁带任务。 磁带类驱动程序作为内核模式 DLL 提供。 为了支持新的磁带设备或磁带系列设备，驱动程序编写器会创建一个特定于设备的磁带 miniclass 驱动程序，该驱动程序将动态链接到系统提供的磁带类驱动程序。

如果磁带 miniclass 驱动程序只调用磁带类驱动程序中的例程，则 miniclass 驱动程序可在支持 Win32 应用程序的 Microsoft 操作系统之间移植，并提供使用磁带 miniclass 接口的磁带类驱动程序。 磁带 miniclass 驱动程序包含头文件 *minitape*。

必须修改现有的磁带 miniclass 驱动程序，以支持一个新的入口点 *TapeMiniGetMediaTypes*，以便在 Windows 2000 和更高版本的操作系统下生成和运行。 不需要任何其他修改。 系统提供的磁带类驱动程序与系统提供的存储端口驱动程序一起，代表磁带 miniclass 驱动程序处理即插即用和电源管理请求。

本部分介绍特定于操作系统的磁带类驱动程序所提供的支持，并提供编写新的磁带 miniclass 驱动程序的准则。

- 有关磁带类和磁带 Miniclass 驱动程序中的例程的详细信息，请参阅 [磁带类驱动程序例程](tape-class-driver-routines.md) 和 [磁带 Miniclass 驱动程序例程](tape-miniclass-driver-routines.md) 。

- 有关存储设备驱动程序层的说明，请参阅 [设备配置和分层驱动程序](../kernel/device-configurations-and-layered-drivers.md) 。
