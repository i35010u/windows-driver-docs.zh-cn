---
title: WDI_TLV_SAE_CONFIRM_REQUEST
description: WDI_TLV_SAE_CONFIRM_REQUEST 是 TLV，其中包含同时进行身份验证的等于 (SAE) 确认请求的参数。
ms.assetid: 9E46D8BA-D359-45B3-8074-FA54F4618E71
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_CONFIRM_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2037de1054b6a4117fbe03a4bddbdf74fb8c5322
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905314"
---
# <a name="wditlvsaeconfirmrequest"></a>WDI_TLV_SAE_CONFIRM_REQUEST

**WDI_TLV_SAE_CONFIRM_REQUEST**是 TLV，其中包含同时进行身份验证的等于 (SAE) 确认请求的参数。 

中的命令参数使用此 TLV [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)。

## <a name="tlv-type"></a>TLV 类型

0x151

## <a name="length"></a>长度

所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | UINT16 |   |   | 发送确认使用的字段，作为抗重播计数器。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | TLV\<LIST\<UINT8>> |  |   | 确认字段中。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
