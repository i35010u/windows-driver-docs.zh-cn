---
title: WDI_TLV_REQUEST_LCI_REPORT
description: WDI_TLV_REQUEST_LCI_REPORT 是一种 TLV，其中包含有关是否应在精细计时度量（INTERNAL.H）请求期间从目标 BSS 请求位置配置信息（LCI）报告的信息。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_REQUEST_LCI_REPORT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6b2ade18e17f79859cc22b9e41e277785b55258a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916893"
---
# <a name="wdi_tlv_request_lci_report"></a>WDI_TLV_REQUEST_LCI_REPORT

**WDI_TLV_REQUEST_LCI_REPORT**是一种 TLV，其中包含有关是否应在精细计时度量（internal.h）请求期间从目标 BSS 请求位置配置信息（LCI）报告的信息。

此 TLV 用于[WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md)。

## <a name="tlv-type"></a>TLV 类型

0x158

## <a name="length"></a>长度

UINT8 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 | 可能的值： <ul><li>0：不需要 LCI 报表。</li><li>1：应请求 LCI 报告。</li></ul> |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
