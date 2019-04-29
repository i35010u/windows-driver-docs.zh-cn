---
title: 创建 IEEE 1394 虚拟设备
description: 创建 IEEE 1394 虚拟设备
ms.assetid: 5b6a4d7a-e116-4a68-a1f8-fd561fbc0495
keywords:
- 仿真驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- 虚拟设备 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e837ada427979c61cd3f3d9ca0da9bc0506581
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376697"
---
# <a name="creating-ieee-1394-virtual-devices"></a>创建 IEEE 1394 虚拟设备





较高级别驱动程序和用户模式服务可以添加或删除 1394年的虚拟设备的设备控制请求通过[ **IOCTL\_IEEE1394\_API\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff537241)控制代码。 该请求包含[ **IEEE1394\_API\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff537204)结构，其**RequestNumber**成员指示要执行 （操作添加或删除） 由总线驱动程序。 由于虚拟设备没有设备 ID 或实例 ID、 驱动程序或请求创建虚拟设备的用户程序，必须提供的设备 ID 和实例中的 ID [ **IEEE1394\_VDEV\_PNP\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff537206)结构。

当 IEEE1394\_请求\_标志\_指定的永久使用 IOCTL\_IEEE1394\_API\_请求，1394年总线驱动程序存储有关非易失性的上下文信息在注册表中的虚拟设备。 这允许自动重新创建在无需从较高级别驱动程序干预下一步启动的虚拟 PDO 总线驱动程序。

总线驱动程序使用此注册表项"枚举"每个 1394年设备堆栈的虚拟设备在系统中。 创建虚拟设备虚拟 PDO 后, 1394年总线驱动程序调用[ **IoInvalidateDeviceRelations**](https://msdn.microsoft.com/library/windows/hardware/ff549353)，只需创建真实的设备，PDO 后像。 此调用通知到达新的设备，插即用 (PnP) 管理器和 PnP 管理器则加载虚拟设备的驱动程序。

如果有多个一个 1394年主机控制器是存在于系统注册表中定义的虚拟设备会超过一次枚举。 若要确保每个虚拟设备具有唯一实例 ID，将创建虚拟设备的高级别的驱动程序或用户服务不应指定"硬编码"的特定实例在具有系统上的虚拟设备的 ID 超过一个 1394年承载控制器。 相反，较高级别软件应设置 IEEE1394\_请求\_标志\_使用\_本地\_主机\_EUI 标志中 IEEE1394\_API\_请求。 如果设置此标志下, 一次总线驱动程序枚举设备，它将使用主控制器的实例 ID，作为虚拟设备的实例 ID。 由于每个 1394年设备堆栈将具有唯一实例 id 的主机控制器，虚拟设备，其实例 ID 是其主控制器的实例 ID 相同，还具有一个唯一实例 id。

若要公开的 1394年总线上的虚拟设备，仿真驱动程序必须添加单元目录的虚拟设备使用以下步骤：

1.  发送[**请求\_设置\_本地\_主机\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff537663)总线驱动程序和对请求**u。SetLocalHostProperties.nLevel** IRB 成员设置为集\_本地\_主机\_属性\_修改\_以便将单元目录添加到系统的 IEEE CROM1394 配置 rom。 此请求还将添加任何其他必要的配置数据到 ROM 的配置以公开仿真的设备功能。 必须使用仿真驱动程序与之关联的虚拟 PDO 发送请求。

2.  发出的总线重置通知存在于系统配置 ROM 已更改的总线上的 1394年节点。

 

 




