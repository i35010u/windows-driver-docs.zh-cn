---
title: 创建 IEEE 1394 虚拟设备
description: 创建 IEEE 1394 虚拟设备
ms.assetid: 5b6a4d7a-e116-4a68-a1f8-fd561fbc0495
keywords:
- 模拟驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- 虚拟设备 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44e398c1fedda4bdd045ff645feaccedb09c3c8a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382259"
---
# <a name="creating-ieee-1394-virtual-devices"></a>创建 IEEE 1394 虚拟设备





上层驱动程序和用户模式服务可以通过使用 [**IOCTL \_ IEEE1394 \_ API \_ 请求**](https://msdn.microsoft.com/library/windows/hardware/ff537241) 控制代码的设备控制请求来添加或删除虚拟1394设备。 请求包含 [**IEEE1394 \_ API \_ 请求**](/previous-versions/ff537204(v=vs.85)) 结构，该结构的 **RequestNumber** 成员指示 (添加或删除总线驱动程序) 执行的操作。 由于虚拟设备没有设备 ID 或实例 ID，因此请求创建虚拟设备的驱动程序或用户程序必须在 [**IEEE1394 \_ VDEV \_ PNP \_ 请求**](https://msdn.microsoft.com/library/windows/hardware/ff537206) 结构中提供设备 id 和实例 ID。

\_ \_ \_ 使用 IOCTL IEEE1394 API 请求指定 IEEE1394 请求标志 PERSISTENT \_ 时 \_ \_ ，1394总线驱动程序会在注册表中存储有关虚拟设备的非易失性上下文信息。 这允许总线驱动程序在下一次启动时自动重新创建虚拟 PDO，而无需从上层驱动程序进行干预。

总线驱动程序使用此注册表项为系统中的每个1394设备堆栈 "枚举" 虚拟设备。 为虚拟设备创建虚拟 PDO 后，1394总线驱动程序会调用 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)，正如为真正的设备创建 PDO 后所做的一样。 此调用通知即插即用 (PnP) 管理器新设备已到达，PnP 管理器加载该虚拟设备的驱动程序。

如果系统中存在 1 1394 个以上的主机控制器，则会多次枚举注册表中定义的虚拟设备。 若要确保每个虚拟设备都具有唯一的实例 ID，则创建虚拟设备的高级驱动程序或用户服务不应为具有 1 1394 个以上主机控制器的系统上的虚拟设备指定特定的 "硬编码" 实例 ID。 相反，高级软件应 \_ \_ \_ \_ \_ \_ 在 IEEE1394 \_ API \_ 请求中设置 IEEE1394 请求标志，使用本地主机的 EUI 标志。 如果设置此标志，则在下一次总线驱动程序枚举设备时，它将使用主机控制器的实例 ID 作为虚拟设备的实例 ID。 由于每个1394设备堆栈将具有一个具有唯一实例 ID 的主机控制器，因此，虚拟设备（其实例 ID 与主机控制器的实例 ID 相同）还将具有唯一的实例 ID。

若要在1394总线上公开虚拟设备，仿真驱动程序必须使用以下步骤为虚拟设备添加单元目录：

1.  向总线驱动程序发送 [**请求 \_ 设置的 \_ 本地 \_ 主机 \_ 属性**](https://msdn.microsoft.com/library/windows/hardware/ff537663) 请求，并将 IRB 设置的 **SetLocalHostProperties. nLevel** 成员设置为设置 \_ 本地 \_ 主机 \_ 属性 \_ MODIFY \_ CROM，以便将单元目录添加到系统的 IEEE 1394 配置 ROM。 此请求还会将任何其他必要的配置数据添加到配置 ROM，以便公开模拟的设备功能。 必须使用仿真驱动程序与之关联的虚拟 PDO 发送请求。

2.  发出总线重置，通知总线上出现系统配置 ROM 更改的1394节点。

 

