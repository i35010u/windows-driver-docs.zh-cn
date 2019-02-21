---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE
description: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE 是包含特定于设备服务的操作码 TLV。
ms.assetid: A0C9E728-E0E5-47C1-AEB8-E001057FA35A
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 75c1152c85fb382c27db8610af7f735b156c2710
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554836"
---
# <a name="wditlvdeviceserviceparamsopcode"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE

WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE 是包含特定于设备服务的操作码 TLV。 在中使用此 TLV [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x13F

## <a name="length"></a>长度

以字节为单位，超出 UINT8 的大小。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| TLV\<UINT8\> | 设备服务特定的操作码。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1809 |
| 最低受支持的服务器 | Windows Server 2016 |
| 标头 | Wditypes.hpp |
