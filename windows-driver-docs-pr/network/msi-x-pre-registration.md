---
title: MSI-X 预先注册
description: MSI-X 预先注册
ms.assetid: 93a09ebd-8a50-4c96-a926-54bb4686a618
keywords:
- MSI X WDK 网络、 资源要求 filter 函数
- 消息信号中断 WDK 网络资源要求筛选器函数
- Msi WDK 网络资源要求筛选器函数
- 资源要求 filter 函数 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf46946b8d5258894f1b6aca5093d41a06c4af65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382639"
---
# <a name="msi-x-pre-registration"></a>MSI-X 预先注册





若要支持不断变化的 MSI X 的中断关联或删除消息中断资源，微型端口驱动程序必须建立资源要求筛选器函数。 在 NDIS 调用之前发生的此预注册步骤[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

若要建立资源要求筛选器函数，微型端口驱动程序必须提供[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数。 当微型端口驱动程序调用[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数从[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，则驱动程序为传递的入口点*MiniportSetOptions*中[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构。 NDIS 调用*MiniportSetOptions*的上下文中的函数**NdisMRegisterMiniportDriver**。

从*MiniportSetOptions*，微型端口驱动程序调用[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数，并指定[ **NDIS\_微型端口\_PNP\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566475)结构。 此结构定义的入口点[ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332)， [ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)， [ *MiniportStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559452)，并[ *MiniportFilterResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff559384)函数。

NDIS 时 NDIS 接收来自插即用 (PnP) 管理器的添加设备请求，调用微型端口驱动程序*MiniportAddDevice*函数。 NDIS 将传递给的句柄*MiniportAddDevice*中*MiniportAdapterHandle*参数是 NDIS 更高版本将传递给句柄[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

在中[ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332)，该驱动程序初始化[ **NDIS\_微型端口\_添加\_设备\_注册\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565945)结构，并将传递到此结构[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。 NDIS\_微型端口\_添加\_设备\_注册\_特性结构包含**MiniportAddDeviceContext**是微型端口的句柄的成员设备的驱动程序分配的上下文区域。 NDIS 更高版本提供了此上下文句柄[ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)， [ *MiniportFilterResourceRequirements*](https://msdn.microsoft.com/library/windows/hardware/ff559384)， [*MiniportStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559452)，和[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 有关*MiniportInitializeEx*，在传递上下文句柄**MiniportAddDeviceContext**的成员[ **NDIS\_微型端口\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565972)结构的*MiniportInitParameters*参数指向。

在 NDIS 后调用[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)并*MiniportAddDevice*返回 NDIS\_状态\_成功后，NDIS 调用*MiniportFilterResourceRequirements*函数，每当它收到[ **IRP\_MN\_筛选器\_资源\_要求** ](https://msdn.microsoft.com/library/windows/hardware/ff550874) I/O 请求数据包 (IRP)。 *MiniportFilterResourceRequirements*可以更改每个 MSI X 消息中断关联、 添加消息中断资源，或删除消息中断资源，如果驱动程序将注册，以便在基于行的中断[*MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 有关建立中断关联策略的详细信息，请参阅[MSI X 资源筛选](msi-x-resource-filtering.md)。

NDIS NDIS 收到删除设备请求时从 PnP 管理器，当调用微型端口驱动程序的[ *MiniportRemoveDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559427)函数。 *MiniportRemoveDevice*函数应撤消操作的[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)函数执行。

 

 





