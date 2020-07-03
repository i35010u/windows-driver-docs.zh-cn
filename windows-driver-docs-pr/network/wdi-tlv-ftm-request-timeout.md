---
title: WDI_TLV_FTM_REQUEST_TIMEOUT
description: WDI_TLV_FTM_REQUEST_TIMEOUT 是一种 TLV，其中包含完成精确计时度量值（INTERNAL.H）所用的最长时间（以毫秒为单位）。
ms.assetid: C2C4CDEE-4CB6-49C1-8DBF-4A1AE71954ED
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_REQUEST_TIMEOUT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bd2b64133a71087cb89c201cffaa07c757fdaa64
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916147"
---
# <a name="wdi_tlv_ftm_request_timeout"></a>WDI_TLV_FTM_REQUEST_TIMEOUT

**WDI_TLV_FTM_REQUEST_TIMEOUT**是一种 TLV，其中包含完成精确计时度量值（internal.h）所用的最长时间（以毫秒为单位）。

此 TLV 用于[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)的任务参数中。

## <a name="tlv-type"></a>TLV 类型

0x161

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT32 | 完成 INTERNAL.H 的最长时间（以毫秒为单位）。 超时值设置为150毫秒，乘以目标的数目。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
