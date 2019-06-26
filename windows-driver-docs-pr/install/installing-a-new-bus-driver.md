---
title: 安装新总线驱动程序
description: 安装新总线驱动程序
ms.assetid: 449c0c08-c995-4e23-a770-a567bd48966c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d4e4207f2d5e97da6c4504b15723bea4a8d3809
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379453"
---
# <a name="installing-a-new-bus-driver"></a>安装新总线驱动程序


新的供应商总线驱动程序应遵守以下准则，用于报告的总线类型和设备 Id，并在可能创建一个新[设备安装程序类](device-setup-classes.md)总线上的子设备。 如果配置或操作的总线和其子设备存在显著差异其他总线，这些指南适用于新的供应商总线。 在这些情况下，新的供应商总线驱动程序应执行以下操作来确保，在总线和其子设备不会无意中并不恰当地分组与其他总线和子设备：

1.  使用唯一的 GUID 来标识总线类型。 总线驱动程序报告子设备的总线类型 (表示为物理设备对象 (*PDO*) 以响应[ **IRP_MN_QUERY_BUS_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)为请求子设备。 此类请求的响应，总线驱动程序返回一个指向[ **PNP_BUS_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pnp_bus_information)结构，它返回中的 GUID **PNP_BUS_INFORMATION。BusTypeGuid**成员。 此外，总线驱动程序应设置**PNP_BUS_INFORMATION。LegacyBusType**到**PNPBus**，和**PNP_BUS_INFORMATION。BusNumber**为适当的自定义值。

2.  使用自定义硬件 Id 和总线子设备。

3.  如果在总线子设备不属于的现有[设备安装程序类](device-setup-classes.md)，[安装新设备安装程序类子设备的总线](installing-a-new-device-setup-class-for-a-bus.md)。

 

 





