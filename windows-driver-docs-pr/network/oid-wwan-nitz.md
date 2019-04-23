---
title: OID_WWAN_NITZ
description: OID_WWAN_NITZ 用于查询当前的网络时间与网络标识和时区 (NITZ)。
ms.assetid: 5AC5842E-CBD1-47E0-88D2-D3F58CC6F142
ms.date: 04/11/2019
keywords:
- 从 Windows Vista 开始 OID_WWAN_NITZ 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9e46b361ddabc0a5f684ca4850972f0a2e99c614
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905261"
---
# <a name="oidwwannitz"></a>OID_WWAN_NITZ

OID_WWAN_NITZ 用于查询当前的网络时间与网络标识和时区 (NITZ)。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)状态通知包含[ **NDIS_WWAN_NITZ_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)结构，描述当前网络时间和时区。

不适用集发出的请求。

## <a name="remarks"></a>备注

有关此 OID 的使用情况的详细信息，请参阅[MB NITZ 支持](mb-nitz-support.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB NITZ 支持](mb-nitz-support.md)

[NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)
