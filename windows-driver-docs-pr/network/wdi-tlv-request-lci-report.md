---
title: WDI_TLV_REQUEST_LCI_REPORT
description: WDI_TLV_REQUEST_LCI_REPORT 是一种 TLV，其中包含有关是否应在精确计时度量 (INTERNAL.H) 请求期间从目标 BSS 请求位置配置信息 (LCI) 报表。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_REQUEST_LCI_REPORT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 79786fea286094308f5aec5fe8f80005420116da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818019"
---
# <a name="wdi_tlv_request_lci_report"></a>WDI_TLV_REQUEST_LCI_REPORT

**WDI_TLV_REQUEST_LCI_REPORT** 是一种 TLV，其中包含有关是否应在精确计时度量 (internal.h) 请求期间从目标 BSS 请求位置配置信息 (LCI) 报表。

此 TLV 用于 [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md)。

## <a name="tlv-type"></a>TLV 类型

0x158

## <a name="length"></a>长度

UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT8 | 可能的值： <ul><li>0：不需要 LCI 报表。</li><li>1：应请求 LCI 报告。</li></ul> |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
