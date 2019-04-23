---
title: WDI_TLV_LCI_REPORT_BODY
description: WDI_TLV_LCI_REPORT_BODY 是包含正常计时 Measuremement (FTM) 请求位置配置报表 (LCI) TLV。
ms.assetid: D80AB500-0B4F-47AC-ADF7-DDB5635FF1F2
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_LCI_REPORT_BODY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6d92d7859feeac6e27efacab4574968369737bb1
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905307"
---
# <a name="wditlvlcireportbody"></a>WDI_TLV_LCI_REPORT_BODY

**WDI_TLV_LCI_REPORT_BODY**是包含正常计时 Measuremement (FTM) 请求位置配置报表 (LCI) TLV。

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x160

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | LCI 报表中。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
