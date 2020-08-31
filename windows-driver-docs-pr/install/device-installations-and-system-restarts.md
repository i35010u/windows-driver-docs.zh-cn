---
title: 设备安装和系统重启
description: 设备安装和系统重启
ms.assetid: c09d2150-60ae-4912-86f5-6489c818853e
keywords:
- 设备安装 WDK，重新启动
- 安装设备 WDK，重新启动
- 设备设置 WDK 设备安装，重新启动
- 重新启动 WDK 设备安装
- 在设备安装过程中启动重新启动
- 在设备安装过程中重启
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c029e12417822d16fc1a6d03ddfe0c81414c962b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095855"
---
# <a name="device-installations-and-system-restarts"></a>设备安装和系统重启





除非绝对必要，否则设备安装不应强制用户重新启动系统。 下列情况下，系统会根据需要重新启动系统：

<a href="" id="installing-or-removing-a-non-plug-and-play-device--"></a>安装或删除非即插即用设备。   
对于这些较早版本的设备，用户通常必须在物理添加或删除设备之前关闭系统。 重新打开电源后，系统启动。

**注意**   无论用户是在插入硬件之前还是之后安装驱动程序，设备的安装程序文件都不应启动系统重新启动。

 

<a href="" id="updating-a-driver-for-a-system-boot-device--"></a>正在为系统启动设备更新驱动程序。   
如果设备可能包含系统的分页、休眠或故障转储文件，则其驱动程序必须为 [**IRP_MN_DEVICE_USAGE_NOTIFICATION**](../kernel/irp-mn-device-usage-notification.md) 请求服务。 系统会先发送此请求，然后再将其中一个文件放在磁盘上。 如果驱动程序成功执行请求，则这些驱动程序必须将所有后续 [**IRP_MN_QUERY_REMOVE_DEVICE**](../kernel/irp-mn-query-remove-device.md) 请求失败。 当设备的驱动程序无法 IRP_MN_QUERY_REMOVE_DEVICE 请求时，系统将提示用户重新启动系统。

**注意**   设备的安装程序文件不应启动系统重新启动。

 

<a href="" id="installing-a-non-wdm-filter-driver-"></a>安装非 WDM 筛选器驱动程序。  
如果将筛选器驱动程序添加到非 WDM 驱动程序堆栈中，则必须重新启动系统。 在这种情况下，驱动程序的安装程序或共同安装程序应请求重新启动系统 (参阅 [在设备安装过程中启动系统重](initiating-system-restarts-during-device-installations.md) 启) 。

**注意**   将筛选器驱动程序添加到 WDM 驱动程序堆栈不需要重新启动系统，除非基础设备是系统引导设备。

 

部分包括以下主题：

[设备安装过程中避免系统重启](avoiding-system-restarts-during-device-installations.md)

[设备安装过程中开始系统重启](initiating-system-restarts-during-device-installations.md)

 

