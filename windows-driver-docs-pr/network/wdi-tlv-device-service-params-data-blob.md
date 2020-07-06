---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB
description: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 是一种 TLV，其中包含有关从 IHV 驱动程序收到的设备服务的信息。
ms.assetid: D07CDC24-849F-447A-8447-FD2D37178C42
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 53ed36aa0bc80fdb79c114211d97d7a9864946e7
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968440"
---
# <a name="wdi_tlv_device_service_params_data_blob"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB

WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 是一种 TLV，其中包含有关从 IHV 驱动程序收到的设备服务的信息。 此 TLV 用于[NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x141

## <a name="length"></a>长度

的大小（以字节为单位） `(UINT8 * (the number of elements in the list))` 。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| TLV\<List\<UINT8\>\> | 可有可无从 IHV 驱动程序接收的信息。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1809

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

