---
title: WDI_TLV_LCI_REPORT_BODY
description: WDI_TLV_LCI_REPORT_BODY 是一种 TLV，其中包含用于精细计时 Measuremement (INTERNAL.H) 请求的位置配置报告 (LCI) 。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_LCI_REPORT_BODY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1209fc6f1db3b6c5589ee2b7fd4383404109d7f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809877"
---
# <a name="wdi_tlv_lci_report_body"></a>WDI_TLV_LCI_REPORT_BODY

**WDI_TLV_LCI_REPORT_BODY** 是一种 TLV，其中包含用于精细计时 MEASUREMEMENT (internal.h) 请求的位置配置报告 (LCI) 。

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x160

## <a name="length"></a>长度

UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT8 [] | LCI 报表。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
