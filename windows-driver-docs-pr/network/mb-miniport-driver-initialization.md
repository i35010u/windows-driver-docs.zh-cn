---
title: MB 微型端口驱动程序初始化
description: MB 微型端口驱动程序初始化
ms.assetid: cf332eb4-faea-40e3-b313-512f81718267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9fa73ca04d98e4fb0b848fccb19f187420ced88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524834"
---
# <a name="mb-miniport-driver-initialization"></a>MB 微型端口驱动程序初始化


下图表示执行来确定接口是否限定为 MB 接口并收集有关设备功能的信息的过程。 MB 服务启动时，以及与每个新的接口到达服务运行时的每个枚举 MB 接口执行这些步骤。 粗体表示 OID 标识符或事务流控制中的标签和中常规文本的标签表示 OID 结构中的重要标志。

![说明建立接口受限定为 mb 接口，并举例说明收集有关设备功能的信息的关系图](images/wwandriverinitproc.png)

若要初始化 MB 微型端口驱动程序，请使用以下过程：

1.  MB 服务发送同步 （阻塞） [OID\_代\_物理\_中等](https://msdn.microsoft.com/library/windows/hardware/ff569621)查询请求以确定的 MB 设备类型。 微型端口驱动程序使用响应**NdisPhysicalMediumWirelessWan**以指示 MB 设备是 WWAN 设备。

2.  MB 服务发送同步 （阻塞） [OID\_代\_媒体\_支持](https://msdn.microsoft.com/library/windows/hardware/ff569609)微型端口驱动程序的查询请求以确定哪种中等 MB 设备使用。 微型端口驱动程序使用响应**NdisMedium802\_3**以指示它使用以太网仿真。

3.  MB 服务发送同步 （阻塞） [OID\_WWAN\_驱动程序\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569825)查询请求来确定哪些驱动程序模型版本的微型端口驱动程序微型端口驱动程序支持。 微型端口驱动程序会使用 WWAN 进行响应\_版本。

4.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_设备\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569824)微型端口驱动程序的查询请求来标识 MB 设备的功能。 微型端口驱动程序使用临时确认响应，它已收到请求，并且它将发送包含所需的信息在将来的通知。

5.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_设备\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff567845)到指示的功能的 MB 服务通知MB 设备微型端口驱动程序支持。 例如，如果微型端口驱动程序支持基于 GSM 的设备，还应指定**WwanCellularClassGsm**中的值**DeviceCaps.WwanCellularClass**的成员[ **NDIS\_WWAN\_设备\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567907)结构。 如果微型端口驱动程序支持基于 CDMA 的设备，还应指定**WwanCellularClassCdma**。

 

 





