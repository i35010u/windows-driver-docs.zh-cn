---
title: WDI_TLV_LCI_REPORT_BODY
description: WDI_TLV_LCI_REPORT_BODY 是一种 TLV，其中包含精细计时 Measuremement （INTERNAL.H）请求的位置配置报告（LCI）。
ms.assetid: D80AB500-0B4F-47AC-ADF7-DDB5635FF1F2
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_LCI_REPORT_BODY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6197c77ce1c54ba0038ff198828f595ebf4ab12c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916107"
---
# <a name="wdi_tlv_lci_report_body"></a>WDI_TLV_LCI_REPORT_BODY

**WDI_TLV_LCI_REPORT_BODY**是一种 TLV，其中包含精细计时 MEASUREMEMENT （internal.h）请求的位置配置报告（LCI）。

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x160

## <a name="length"></a>长度

UINT8 元素数组的大小（以字节为单位）。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 [] | LCI 报表。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
