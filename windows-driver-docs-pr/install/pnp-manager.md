---
title: Plug and Play 管理器
description: Plug and Play 管理器
ms.assetid: b1890b3c-fc7b-4a2e-b48a-8266f237c9b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764aaec910426cfcd64be2d82838bc3b8e10f155
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525455"
---
# <a name="plug-and-play-manager"></a>Plug and Play 管理器


Plug and Play (PnP) 管理器中 Windows 即插即用功能提供支持，并负责以下 PnP 相关的任务：

-   设备检测和枚举期间启动系统

-   添加或删除设备，系统运行时

新设备的系统上存在并且必须安装，内核模式即插即用管理器将通知用户模式即插即用管理器。

内核模式即插即用管理器还会调用[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)并[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程的设备的驱动程序，并将发送[**执行了 IRP_MN_START_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551749)启动设备的请求。

PnP 管理器维护[设备树](https://msdn.microsoft.com/library/windows/hardware/ff543194)，会跟踪系统中的设备。 设备树包含系统上存在的设备的相关信息。 在计算机启动时，PnP 管理器使用的驱动程序和其他组件的信息生成此树，并更新树，如添加或删除设备。

 

 





