---
title: 删除 IEEE 1394 虚拟设备
description: 删除 IEEE 1394 虚拟设备
ms.assetid: ea2d4b9e-7774-42dc-98dd-d95298012d72
keywords:
- 仿真驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- 虚拟设备 WDK IEEE 1394 总线
- 删除虚拟设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f37fcbd77653fcc4e0b7b34931265a595758766
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544011"
---
# <a name="removing-ieee-1394-virtual-devices"></a>删除 IEEE 1394 虚拟设备





有两个删除的虚拟设备的物理设备对象 (PDO) 的方法：

1.  **标准插设置 （即插即用） 的方法删除设备**。 若要使用此方法，具有您的驱动程序发送[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)到虚拟设备的请求。

    I/O 堆栈应包含以下值：

    -   **MajorFunction** = IRP\_MJ\_PNP
    -   **MinorFunction** = IRP\_MN\_删除\_设备

2.  **类型的 I/O 请求数据包 (IRP)** IOCTL\_IEEE1394\_API\_请求：若要使用此方法，具有您的驱动程序发送[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)到虚拟设备的请求。

    I/O 堆栈应包含以下值：

    -   **MajorFunction** = IRP\_MJ\_设备\_控件
    -   **Parameters.DeviceIoControl.IoControlCode** = [**IOCTL\_IEEE1394\_API\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff537241)

    IRP 应包含以下值：

    -   **AssocicatedIrp.SystemBuffer-&gt;SystemBuffer**指向[ **IEEE1394\_API\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff537204)结构
    -   **RequestNumber**隶属 IEEE1394\_API\_请求 = [ **IEEE1394\_API\_删除\_虚拟\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff537201)

第一种方法 (IRP\_MN\_删除\_设备) 会移除该设备，但如果是持久性的设备将恢复下一次计算机启动。 第二种方法 (IEEE1394\_API\_删除\_虚拟\_设备)，以便它将不再保留在重新启动后完全删除该设备。 下一次在计算机启动该设备将不会还原。

请注意，较高级别驱动程序或用户模式服务可以确定，通过常规的即插即用机制，已列出的虚拟设备。 此机制使用的虚拟驱动程序的 INF 文件中的类提供的 GUID。

 

 




