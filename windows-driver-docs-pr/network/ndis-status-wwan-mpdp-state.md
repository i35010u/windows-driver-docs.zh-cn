---
title: NDIS_STATUS_WWAN_MPDP_STATE
description: 移动宽带的微型端口驱动程序发送 NDIS_STATUS_WWAN_MPDP_STATE 通知以以前 OID_WWAN_MPDP 集请求的完成情况通知给 MB 服务。
ms.assetid: 59B8D9A0-FB22-4252-A24B-A9E58B068C4E
keywords:
- NDIS_STATUS_WWAN_MPDP_STATE，与 Windows Vista 一起启动的网络驱动程序
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MPDP_STATE
api_location:
- ndis.h
api_type:
- HeaderDef
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: f756200c7f49dbcf77a24e2f72903f58570a40bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369894"
---
# <a name="ndisstatuswwanmpdpstate"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE**移动宽带的微型端口驱动程序发送通知来告知在前一次完成 MB 服务[OID_WWAN_MPDP](oid-wwan-mpdp.md)集请求。

为未经请求的事件不发送此通知。

使用此通知[ **NDIS_WWAN_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1809 |
| Header | Ndis.h |
