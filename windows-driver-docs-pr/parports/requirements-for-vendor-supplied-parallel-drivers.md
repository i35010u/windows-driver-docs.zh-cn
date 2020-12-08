---
title: 对供应商提供的并行驱动程序的要求
description: 对供应商提供的并行驱动程序的要求
keywords:
- 供应商提供的并行驱动程序 WDK，关于供应商提供的并行驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c26be7d8be88cf30981e793960be8ac0f4006892
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806089"
---
# <a name="requirements-for-vendor-supplied-parallel-drivers"></a>对供应商提供的并行驱动程序的要求





本部分介绍针对供应商提供的用于并行端口和设备连接到并行端口的驱动程序的 Microsoft Windows 要求。

不需要供应商提供的并行端口的函数驱动程序和总线驱动程序，因为 [系统提供的并行驱动](system-supplied-parallel-drivers.md) 程序提供了这些功能。 系统提供的并行驱动程序为附加到并行端口的操作并行端口和设备提供了广泛的支持。

供应商为连接到并行端口的并行设备提供的函数驱动程序是可选的。 系统提供的并行驱动程序为直接控制作为原始设备的并行设备以及操作设备的父并行端口提供了广泛的支持。

如果供应商为并行设备提供函数驱动程序，则该驱动程序必须支持即插即用和电源管理。 Microsoft 建议驱动程序为 WDM 驱动程序。

以下主题介绍供应商为并行设备提供的函数驱动程序如何操作设备和设备的父并行端口：

[打开并行端口](operating-a-parallel-port.md)

[打开连接到并行端口的并行设备](operating-a-parallel-device-attached-to-a-parallel-port.md)

 

 




