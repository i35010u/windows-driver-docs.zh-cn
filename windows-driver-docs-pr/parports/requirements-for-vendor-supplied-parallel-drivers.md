---
title: 对供应商提供的并行驱动程序的要求
description: 对供应商提供的并行驱动程序的要求
ms.assetid: 2194ad1a-3548-4b67-9268-4245389cf264
keywords:
- 供应商提供并行的驱动程序 WDK，有关供应商提供并行的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67da7d07a26993d6abedab3777478bef20e2340
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377216"
---
# <a name="requirements-for-vendor-supplied-parallel-drivers"></a>对供应商提供的并行驱动程序的要求





本部分介绍 Microsoft Windows 要求的供应商提供的并行端口和并行端口连接的设备的驱动程序。

供应商提供的函数驱动程序和并行端口的总线驱动程序不需要，因为[系统提供并行的驱动程序](system-supplied-parallel-drivers.md)提供这些函数。 系统提供的并行驱动程序提供对操作系统的并行端口和并行端口连接的设备的广泛支持。

供应商提供的函数的并行连接到并行端口的设备的驱动程序是可选的。 系统提供的并行驱动程序提供广泛支持用于直接控制为原始的设备，并行设备和操作系统的设备的父并行端口。

如果供应商为并行设备提供了功能驱动程序，该驱动程序必须支持插和电源管理。 Microsoft 建议使用该驱动程序是 WDM 驱动程序。

以下主题介绍了在设备和设备的父并行端口并行设备的供应商提供的函数驱动程序的运行方式：

[运行并行端口](operating-a-parallel-port.md)

[运行并行设备附加到并行端口](operating-a-parallel-device-attached-to-a-parallel-port.md)

 

 




