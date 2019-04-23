---
title: WDI_TLV_SAE_REQUEST_TYPE
description: WDI_TLV_SAE_REQUEST_TYPE 是包含类型的同时进行身份验证的等于 (SAE) 请求帧发送到目标 BSSID TLV。
ms.assetid: 90F0F7DA-DACA-49EF-86E8-CE4206D83882
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_REQUEST_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8bff2419cd0812bd81c0f462218fcd52c77b5d13
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905269"
---
# <a name="wditlvsaerequesttype"></a>WDI_TLV_SAE_REQUEST_TYPE

**WDI_TLV_SAE_REQUEST_TYPE**是包含类型的同时进行身份验证的等于 (SAE) 请求帧发送到目标 BSSID TLV。

中的命令参数使用此 TLV [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)。

## <a name="tlv-type"></a>TLV 类型

0x14F

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_request_type) | SAE 请求帧为 bssid 时发送的类型。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
