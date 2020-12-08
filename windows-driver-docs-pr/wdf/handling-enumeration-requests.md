---
title: 处理枚举请求
description: 处理枚举请求
keywords:
- 枚举 WDK KMDF
- PnP WDK KMDF，总线枚举
- 即插即用 WDK KMDF，总线枚举
- 总线枚举 WDK KMDF
- 列出子设备 WDK KMDF
- 子设备 WDK KMDF
- 动态枚举 WDK KMDF
- 静态枚举 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b9c035ecbfb3feea7a306ffbe254cbd89c68b82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814747"
---
# <a name="handling-enumeration-requests"></a>处理枚举请求


PnP 管理器可以随时请求总线驱动程序枚举其子级。  (如果你熟悉 WDM 接口，则枚举请求为 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](../kernel/irp-mn-query-device-relations.md) 请求，其关系类型为 **BusRelations**。 ) 基于框架的驱动程序不会看到这些请求。 而是通过使用存储在设备的子列表中的信息来处理请求。 驱动程序负责使子列表保持最新状态，以便在 PnP 经理请求枚举时，框架可以提供正确的信息。

支持动态枚举的基于框架的总线驱动程序可以接收 reenumerate 特定子设备的请求。 当驱动程序检测到设备故障后，子设备的函数驱动程序可能会发送此类请求。  (框架支持此类请求，方法是实现 [**REENUMERATE \_ \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reenumerate_self_interface_standard)接口，该接口是在 *wdm* 中定义的标准 [驱动程序定义接口](using-driver-defined-interfaces.md)。 ) 

支持动态枚举的基于框架的总线驱动程序可以提供一个 [*EvtChildListDeviceReenumerated*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_device_reenumerated) 回调函数，框架在从子设备的驱动程序收到 reenumeration 请求时调用该函数。 如果此回调函数返回 **TRUE** 或不存在，则框架会将子设备标记为不再存在，并通知 PnP 管理器总线驱动程序的子列表已更改。 因此，PnP 管理器会请求 reenumeration，框架将调用驱动程序的 [*EvtChildListCreateDevice*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) 回调函数，该函数将为子设备创建新的 PDO。

 

