---
title: MB 微型端口驱动程序初始化
description: MB 微型端口驱动程序初始化
ms.assetid: cf332eb4-faea-40e3-b313-512f81718267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5bd44f978644a08ce3f9f16c18a5372d3901ad7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207465"
---
# <a name="mb-miniport-driver-initialization"></a>MB 微型端口驱动程序初始化


下图显示了确定接口是否被限定为 MB 接口以及收集有关设备功能的信息所执行的过程。 当启动 MB 服务时，将为每个枚举的 MB 接口执行这些步骤，并在服务运行时针对每个新的接口到达执行这些步骤。 以粗体显示的标签表示 OID 标识符或事务流控制，而常规文本中的标签表示 OID 结构中的重要标志。

![说明如何在接口被限定为 mb 接口的情况下建立的关系图，并说明如何收集有关设备功能的信息](images/wwandriverinitproc.png)

若要初始化 MB 微型端口驱动程序，请使用以下过程：

1.  MB 服务发送同步 (阻塞) OID 生成 [ \_ \_ 物理 \_ 中型](./oid-gen-physical-medium.md) 查询请求来识别 MB 设备的类型。 微型端口驱动程序通过 **NdisPhysicalMediumWirelessWan** 进行响应，以指示 MB 设备为 WWAN 设备。

2.  MB 服务向微型端口驱动程序发送同步 (阻止) [OID 生成 \_ \_ 媒体 \_ 支持](./oid-gen-media-supported.md) 的查询请求，以确定 MB 设备使用的介质类型。 微型端口驱动程序使用 **NdisMedium802 \_ 3** 进行响应，以指示它使用以太网模拟。

3.  MB 服务向微型端口驱动程序发送同步 (阻止) [OID \_ WWAN \_ 驱动程序 \_ cap](./oid-wwan-driver-caps.md) 查询请求，以确定微型端口驱动程序支持的驱动程序型号版本。 微型端口驱动程序以 WWAN \_ 版本响应。

4.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 设备 \_ cap](./oid-wwan-device-caps.md) 查询请求，以确定 MB 设备的功能。 微型端口驱动程序使用其收到请求的临时确认进行响应，并且它将在将来发送包含所需信息的通知。

5.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 设备 \_ Cap**](./ndis-status-wwan-device-caps.md) 通知发送到 mb 服务，该服务指示微型端口驱动程序支持的 mb 设备的功能。 例如，如果微型端口驱动程序支持基于 GSM 的设备，则它应在[**NDIS \_ WWAN \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构的**DeviceCaps. WwanCellularClass**成员中指定**WwanCellularClassGsm**值。 如果微型端口驱动程序支持基于 CDMA 的设备，则应指定 **WwanCellularClassCdma**。

 

