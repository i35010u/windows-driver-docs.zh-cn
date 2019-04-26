---
title: NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 状态指示要传递给用户模式下客户端提供设备的未经请求信息。
ms.assetid: 6A9EA354-86F0-4C3F-974E-4FC164239D6A
ms.date: 06/14/2018
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 28c22b0e161cd002c06548486f9b01ab59437d2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330551"
---
# <a name="ndisstatuswdiindicationdeviceserviceevent"></a>NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT

IHV 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 状态指示要传递给用户模式下客户端提供设备的未经请求信息。

设备服务指示必须发送的微型端口驱动程序中的时，才*D0*电源状态，并且它必须不会导致设备从唤醒*Dx*。 WDI 将删除此指示，但如果它收到在堆栈中向上转发不在*Dx*。

此指示当前处理仅在默认端口 （工作站） 上。

微型端口驱动程序应发送单独为每个设备服务 GUID 和操作码对根据需要随时通知。

## <a name="payload-data"></a>有效负载数据

| 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB](wdi-tlv-device-service-params-data-blob.md) |   | X | 从 IHV 微型端口驱动程序收到的信息。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_GUID](wdi-tlv-device-service-params-guid.md) |   |   | 标识此指示所属 （如 IHV/OEM 所定义） 的设备服务的 GUID。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE](wdi-tlv-device-service-params-opcode.md) |   |   | 设备服务特定的操作码。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1809 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |
