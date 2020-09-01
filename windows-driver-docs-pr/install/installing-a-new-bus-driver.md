---
title: 安装新总线驱动程序
description: 安装新总线驱动程序
ms.assetid: 449c0c08-c995-4e23-a770-a567bd48966c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2febca3ce009577112da1447cac22c65f26d54df
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097289"
---
# <a name="installing-a-new-bus-driver"></a>安装新总线驱动程序


新供应商总线驱动程序应遵循以下指导原则来报告总线类型和设备 Id，以及为总线上的子设备创建新的 [设备安装程序类](./overview-of-device-setup-classes.md) 。 如果总线及其子设备的配置或操作与其他总线相比明显不同，则这些指导原则适用于新的供应商总线。 在这些情况下，新的供应商总线驱动程序应执行以下操作，以确保不会无意中将总线及其子设备与其他总线和子设备进行了不当组合：

1.  使用唯一的 GUID 来标识总线类型。 总线驱动程序报告子设备的总线类型 (表示为 (*PDO*) 的物理设备对象，以响应对子设备的 [**IRP_MN_QUERY_BUS_INFORMATION**](../kernel/irp-mn-query-bus-information.md) 请求。 作为此类请求的响应，总线驱动程序将返回一个指向 [**PNP_BUS_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information) 结构的指针，该结构返回 PNP_BUS_INFORMATION 中的 GUID **。BusTypeGuid** 成员。 此外，总线驱动程序应设置 **PNP_BUS_INFORMATION。LegacyBusType** 到 **PNPBus**，并 **PNP_BUS_INFORMATION。BusNumber** 到适当的自定义值。

2.  使用总线的自定义硬件 Id 和子设备。

3.  如果总线的子设备不属于现有的 [设备安装程序类](./overview-of-device-setup-classes.md)，则 [为总线的子设备安装新的设备安装程序类](installing-a-new-device-setup-class-for-a-bus.md)。

 

