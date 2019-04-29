---
title: 旧式微型端口驱动程序的电源管理
description: 旧式微型端口驱动程序的电源管理
ms.assetid: 676c8c4c-3fd7-4063-a704-2bbfdd03a94e
keywords:
- 电源管理 WDK NDIS 微型端口，旧的微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2aab7c0950cea4b5a90376f13365a5cc33b4aa1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388756"
---
# <a name="power-management-for-old-miniport-drivers"></a>旧式微型端口驱动程序的电源管理





NDIS 将视为旧的微型端口驱动程序微型端口驱动程序，它不是电源管理感知如果：

-   在初始化期间，总线驱动程序指示，在系统或 NIC 是电源管理感知。

-   微型端口驱动程序返回 NDIS\_状态\_不受支持的响应[OID\_PNP\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569774)查询。 NDIS 5.1 和更早的微型端口驱动程序或中间驱动程序会收到此 OID 查询。

-   用户禁用用户界面中的电源管理。

NDIS 支持只有两个设备的电源状态的旧的微型端口驱动程序，不支持 power manegement: D3 状态和 highest-powered (D0) 状态。

在初始化期间，旧的微型端口驱动程序可以指示，NDIS 应不来暂停脚本进程之前，系统将转换为休眠 (D3) 状态。 微型端口驱动程序使此类表示通过设置 NDIS\_特性\_否\_暂停\_ON\_中的挂起标志*AttributeFlags*参数，微型端口驱动程序将传递给[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。 旧的微型端口驱动程序应设置此标志仅当它可以：

-   保存它可能需要的所有硬件上下文。

-   NIC 置于休眠状态 (D3) 的相应状态。

-   重新激活到 highest-powered 状态 (D0) NIC。

如果 NIC 不是电源管理注意，如果微型端口驱动程序未设置 NDIS NDIS 确定总线驱动程序从\_特性\_否\_暂停\_ON\_挂起标志将不会查询 NDIS微型端口驱动程序的电源管理功能。 但是，如果微型端口驱动程序设置 NDIS\_特性\_否\_暂停\_ON\_挂起标志、 NDIS 问题[OID\_PNP\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569774)微型端口驱动程序的请求。 在这种情况下，微型端口驱动程序应该会成功 OID\_PNP\_功能请求使用 NDIS\_状态\_成功。 在 NDIS\_PM\_唤醒\_向上\_功能构建到此请求的响应中返回的微型端口驱动程序、 微型端口驱动程序还必须指定设备电源状态的**NdisDeviceStateUnspecified**为每个唤醒功能。

NDIS 查找旧的微型端口驱动程序提供以下的电源管理支持：

-   NDIS 成功所有[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)系统电源管理器向设备发送的请求对象，它表示 nic。 即 NDIS 保证的微型端口驱动程序的 NIC 将转换为 D3 状态以响应任何 IRP\_MN\_查询\_从系统电源请求。

-   如果微型端口驱动程序未设置 NDIS\_特性\_否\_暂停\_ON\_初始化过程中，NDIS 挂起标志调用微型端口驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)之前微型端口驱动程序的 NIC 的函数将转换为状态 D3。 微型端口驱动程序的 NIC 将失去所有硬件上下文信息。

-   如果微型端口驱动程序设置 NDIS\_特性\_否\_暂停\_ON\_初始化过程中，NDIS 挂起标志不会停止之前，系统将转换为状态 D3 的微型端口驱动程序。 相反，NDIS 发出微型端口驱动程序[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780) D3 状态的请求。 微型端口驱动程序必须保存它使用的任何硬件上下文并置于 NIC 状态适用于 D3 状态。

-   虽然系统转换为 S0[系统的电源状态](https://msdn.microsoft.com/library/windows/hardware/ff564571)，NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数 NDIS 停止微型端口驱动程序。 如果 NDIS 微型端口驱动程序不会暂停，NDIS OID 的微型端口驱动程序发出\_PNP\_设置\_POWER D0 状态请求。 微型端口驱动程序必须置于 NIC 状态适用于 D0 状态。

-   如果微型端口驱动程序已停止并重新初始化，NDIS 还原所有适当的微型端口驱动程序设置，如数据包筛选器和多播的地址列表，通过发出 OID 请求。 如果微型端口驱动程序未暂停，然后重新初始化，微型端口驱动程序必须还原此类设置。

 

 





