---
title: OID_WWAN_NITZ
description: OID_WWAN_NITZ 用于使用网络标识和时区 (NITZ) 查询当前网络时间。
ms.date: 04/11/2019
keywords:
- 从 Windows Vista 开始 OID_WWAN_NITZ 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 22198c826fb01331921a12463fc27fcede706af2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809957"
---
# <a name="oid_wwan_nitz"></a>OID_WWAN_NITZ

OID_WWAN_NITZ 用于使用网络标识和时区 (NITZ) 查询当前网络时间。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送 [NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md) 状态通知，其中包含描述当前网络时间和时区的 [**NDIS_WWAN_NITZ_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 结构。

设置请求不适用。

## <a name="remarks"></a>备注

有关此 OID 的用法的详细信息，请参阅 [MB NITZ 支持](mb-nitz-support.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB NITZ 支持](mb-nitz-support.md)

[NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)

[**NDIS_WWAN_NITZ_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)
