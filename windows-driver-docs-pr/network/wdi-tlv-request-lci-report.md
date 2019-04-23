---
title: WDI_TLV_REQUEST_LCI_REPORT
description: WDI_TLV_REQUEST_LCI_REPORT 是包含的信息是否位置配置信息 (LCI) 报表应在正常时间度量 (FTM) 请求期间请求从目标 BSS TLV。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_REQUEST_LCI_REPORT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 70c3c232db4b4dd0930a39df75b67fe02b072bcb
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905326"
---
# <a name="wditlvrequestlcireport"></a>WDI_TLV_REQUEST_LCI_REPORT

**WDI_TLV_REQUEST_LCI_REPORT**是 TLV，其中是否的位置配置信息 (LCI) 报表应在正常时间度量 (FTM) 请求期间从目标 BSS 请求的信息。

在中使用此 TLV [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md)。

## <a name="tlv-type"></a>TLV 类型

0x158

## <a name="length"></a>长度

超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8 | 可能值： <ul><li>0:不需要 LCI 报表。</li><li>1：应请求 LCI 报表。</li></ul> |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
