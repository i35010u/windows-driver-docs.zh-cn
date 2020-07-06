---
title: NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT
description: 小型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 状态指示将有关设备的未经请求的信息传递到用户模式客户端。
ms.assetid: 6A9EA354-86F0-4C3F-974E-4FC164239D6A
ms.date: 06/14/2018
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 618f52d23b1a19e84b64a79ae585e8f269e28ce9
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968130"
---
# <a name="ndis_status_wdi_indication_device_service_event"></a>NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT

IHV 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 状态指示将有关设备的未经请求的信息传递到用户模式客户端。

设备服务指示只有在处于*D0*电源状态时才必须由微型端口驱动程序发送，并且它不能导致设备从*Dx*唤醒。 WDI 将删除此指示，而不*会在堆栈中收到*它时将其转发。

此指示当前仅在默认端口（工作站）上进行处理。

如果需要，微型端口驱动程序应为每个设备服务 GUID 和 opcode 对发送单独的通知。

## <a name="payload-data"></a>负载数据

| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB](wdi-tlv-device-service-params-data-blob.md) |   | X | 从 IHV 微型端口驱动程序接收的信息。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_GUID](wdi-tlv-device-service-params-guid.md) |   |   | 标识此指示所属的设备服务（由 IHV/OEM 定义）的 GUID。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE](wdi-tlv-device-service-params-opcode.md) |   |   | 特定于设备服务的操作码。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1809

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi

