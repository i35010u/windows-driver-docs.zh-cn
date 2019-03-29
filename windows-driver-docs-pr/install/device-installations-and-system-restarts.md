---
title: 设备安装和系统重启
description: 设备安装和系统重启
ms.assetid: c09d2150-60ae-4912-86f5-6489c818853e
keywords:
- 设备安装 WDK，重新启动
- 安装 WDK 的设备，请重新启动
- 设备安装程序 WDK 设备安装，重新启动
- 重新启动 WDK 设备安装
- 设备安装期间启动重新启动
- 设备安装期间重新启动
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c83cde688a8f228979abd2964c4fcf32dd05cafe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563354"
---
# <a name="device-installations-and-system-restarts"></a>设备安装和系统重启





设备安装不应强制用户重新启动系统，除非绝对必要。 在以下情况下是唯一的系统重新启动，才有必要：

<a href="" id="installing-or-removing-a-non-plug-and-play-device--"></a>安装或删除非即插即用设备。   
对于这些更低版本的设备，用户通常必须关闭系统以物理方式添加或删除设备之前。 在重新打开电源后，在系统启动。

**请注意**  设备的安装程序文件不应启动系统重新启动，而不考虑用户是否在之前或之后插入的硬件中安装驱动程序。

 

<a href="" id="updating-a-driver-for-a-system-boot-device--"></a>正在更新系统启动设备的驱动程序。   
如果系统的分页、 休眠或崩溃转储文件，可能可以保留一个设备，其驱动程序必须服务[ **IRP_MN_DEVICE_USAGE_NOTIFICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff550841)请求。 系统将其中一个磁盘上文件之前，先发送此请求。 如果驱动程序请求成功，它们必须失败任何后续[ **IRP_MN_QUERY_REMOVE_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551705)请求。 当设备的驱动程序失败时的 IRP_MN_QUERY_REMOVE_DEVICE 请求时，系统会提示用户重新启动系统。

**请注意**  设备的安装程序文件不应启动系统重新启动。

 

<a href="" id="installing-a-non-wdm-filter-driver-"></a>安装非 WDM 筛选器驱动程序。  
如果筛选器驱动程序添加到非 WDM 驱动程序堆栈，则必须重新启动系统。 在这种情况下，驱动程序的安装程序或辅助安装程序应请求重新启动系统 (请参阅[启动系统重新启动设备安装期间](initiating-system-restarts-during-device-installations.md))。

**请注意**  将筛选器驱动程序添加到 WDM 驱动程序堆栈不需要重新启动系统，除非基础设备是系统启动设备。

 

部分包括以下主题：

[设备安装过程中避免系统重新启动](avoiding-system-restarts-during-device-installations.md)

[设备安装期间启动系统重新启动](initiating-system-restarts-during-device-installations.md)

 

 





