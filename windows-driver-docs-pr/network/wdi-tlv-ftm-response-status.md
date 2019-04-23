---
title: WDI_TLV_FTM_RESPONSE_STATUS
description: WDI_TLV_FTM_RESPONSE_STATUS 是包含的正常时间度量 (FTM) 响应状态，从目标 BSS TLV。
ms.assetid: 49C3759C-3F3F-4C2D-863E-28227ED323BA
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_RESPONSE_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3ad6fe20d99fbf9ffcd408254297807dd9030ab5
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905320"
---
# <a name="wditlvftmresponsestatus"></a>WDI_TLV_FTM_RESPONSE_STATUS

**WDI_TLV_FTM_RESPONSE_STATUS**是包含的正常时间度量 (FTM) 响应状态，从目标 BSS TLV。

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x159

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ftm_response_status) | FTM 响应状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
