---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB
description: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 是一种 TLV，其中包含有关从 IHV 驱动程序收到的设备服务的信息。
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ca37716ceaf68dabf9101c4cacde71f86cc29a40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822005"
---
# <a name="wdi_tlv_device_service_params_data_blob"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB

WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 是一种 TLV，其中包含有关从 IHV 驱动程序收到的设备服务的信息。 此 TLV 用于 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) 状态指示。

## <a name="tlv-type"></a>TLV 类型

0x141

## <a name="length"></a>长度

的大小（以字节为单位） `(UINT8 * (the number of elements in the list))` 。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| TLV\<List\<UINT8\>\> | 可有可无从 IHV 驱动程序接收的信息。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1809

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

