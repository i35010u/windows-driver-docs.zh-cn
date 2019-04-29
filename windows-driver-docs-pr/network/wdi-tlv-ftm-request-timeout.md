---
title: WDI_TLV_FTM_REQUEST_TIMEOUT
description: WDI_TLV_FTM_REQUEST_TIMEOUT 是包含最大时间 （毫秒），以完成正常计时度量 (FTM) TLV。
ms.assetid: C2C4CDEE-4CB6-49C1-8DBF-4A1AE71954ED
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_REQUEST_TIMEOUT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d5f324bf21fbd9ded8949036e63a2e4584ad854e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382889"
---
# <a name="wditlvftmrequesttimeout"></a>WDI_TLV_FTM_REQUEST_TIMEOUT

**WDI_TLV_FTM_REQUEST_TIMEOUT**是包含最大时间 （毫秒），以完成正常计时度量 (FTM) TLV。

中的任务参数使用此 TLV [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)。

## <a name="tlv-type"></a>TLV 类型

0x161

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT32 | 最长的时间，以毫秒为单位，以完成 FTM。 超时设置为 150 毫秒的目标数的乘积。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
