---
title: WDI_TLV_RETRY_AFTER
description: WDI_TLV_RETRY_AFTER 是包含持续时间，以秒为单位，尝试从目标 BSS 请求新的正常时间度量 (FTM) 之前应经过 TLV。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RETRY_AFTER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9c0375d4c9b2f382250606e252c072665f00b69a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360165"
---
# <a name="wditlvretryafter"></a>WDI_TLV_RETRY_AFTER

**WDI_TLV_RETRY_AFTER**是包含持续时间，以秒为单位，尝试从目标 BSS 请求新的正常时间度量 (FTM) 之前应经过 TLV。

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15A

## <a name="length"></a>长度

UINT16 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT16 | 持续时间，以秒为单位，应通过尝试从目标 BSS 请求新的正常时间度量 (FTM) 之前。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
