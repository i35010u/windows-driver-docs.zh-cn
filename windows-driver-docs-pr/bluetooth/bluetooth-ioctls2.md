---
title: 蓝牙 Ioctl
description: 蓝牙 Ioctl
ms.assetid: 384ea4bb-863c-4da7-bf81-85d2de734ef7
keywords:
- 蓝牙 WDK Ioctl
- Ioctl WDK 蓝牙
- 本地蓝牙 WDK
- 远程蓝牙 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eb288aecf802f99cffc26b0184eff1fe67d1fd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525660"
---
# <a name="bluetooth-ioctls"></a>蓝牙 Ioctl


蓝牙驱动程序堆栈提供了具有多个 Ioctl，若要收集其信息的配置文件驱动程序：

-   本地 Bluetooth 无线电收发器和系统中。

-   远程蓝牙设备。

-   导致加载配置文件驱动程序管理器的 Plug and Play (PnP) 设备。

若要收集有关本地 Bluetooth 无线电收发器和系统的信息，请配置文件驱动程序将使用[ **IOCTL\_同时为\_获取\_本地\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536684)。 IOCTL 返回后，将其**AssociatedIrp.SystemBuffer**成员包含一个指向[**同时为\_本地\_单选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536644)结构，其中包含有关本地 Bluetooth 无线电收发器和系统，包括这些标志指示是否是发现并连接到本地的无线电收发器的信息。 返回的同时为\_本地\_单选\_信息结构包含[同时为\_设备\_信息](https://go.microsoft.com/fwlink/p/?linkid=50713)结构，其中包含特定于系统的信息和[**同时为\_单选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536646)结构，其中包含本地单选特定信息。

若要收集有关特定远程蓝牙设备的信息，请配置文件驱动程序将使用[ **IOCTL\_同时为\_获取\_单选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536685)。 IOCTL 返回后，将其**AssociatedIrp.SystemBuffer**成员包含一个指向同时为\_单选\_提供有关特定的远程无线电收发的信息的信息结构包括是否可以发现并连接到远程单选。

若要收集有关已发现的所有远程的无线电收发器的信息，请配置文件驱动程序将使用[ **IOCTL\_同时为\_获取\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536683)。 IOCTL 返回后，将其**AssociatedIrp.SystemBuffer**成员包含一个指向[**同时为\_设备\_信息\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff536642)结构，其中包含的同时为数组\_设备\_信息结构。 同时为\_设备\_信息\_列表结构包含一个数组项的每个已发现远程单选。 用户模式[BluetoothGetDeviceInfo](https://go.microsoft.com/fwlink/p/?linkid=74493) API 使用此功能来返回有关所有远程无线电收发器的信息。

若要收集有关导致 PnP 管理器中，若要加载该远程设备的信息，配置文件驱动程序将使用[ **IOCTL\_内部\_BTHENUM\_获取\_DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff536748). IOCTL 返回后，将其**AssociatedIrp.SystemBuffer**成员包含一个指向同时为\_设备\_信息结构，其中包含有关远程设备，包括其 Bluetooth 的设备的信息地址、 设备状态和其类的设备 (CoD) 设置。

配置文件驱动程序将使用[ **IOCTL\_内部\_BTHENUM\_获取\_ENUMINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff536750)以获取有关基础设备和服务的信息导致要加载的配置文件驱动程序的即插即用管理器。 IOCTL 返回后，将其**AssociatedIrp.SystemBuffer**成员包含一个指向[**同时为\_枚举器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536643)结构包含的供应商提供的信息的设备，包括端口号、 设备标志、 供应商 ID 和产品 id。

有关使用蓝牙 Ioctl 和 BRBs 的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

 

 





