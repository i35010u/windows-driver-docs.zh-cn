---
title: WDI_TLV_FTM_REQUEST_TIMEOUT
description: WDI_TLV_FTM_REQUEST_TIMEOUT 是一种 TLV，其中包含 (INTERNAL.H) 完成精细计时度量的最长时间（以毫秒为单位）。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_REQUEST_TIMEOUT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2b7a3dbefb0cd7a0db08e43dc57cdd77d028d4fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825361"
---
# <a name="wdi_tlv_ftm_request_timeout"></a>WDI_TLV_FTM_REQUEST_TIMEOUT

**WDI_TLV_FTM_REQUEST_TIMEOUT** 是一种 TLV，其中包含 (internal.h) 完成精细计时度量的最长时间（以毫秒为单位）。

此 TLV 用于 [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)的任务参数中。

## <a name="tlv-type"></a>TLV 类型

0x161

## <a name="length"></a>长度

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT32 | 完成 INTERNAL.H 的最长时间（以毫秒为单位）。 超时值设置为150毫秒，乘以目标的数目。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
