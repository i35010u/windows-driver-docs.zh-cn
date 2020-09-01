---
title: NDIS_STATUS_WWAN_MPDP_STATE
description: NDIS_STATUS_WWAN_MPDP_STATE 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个 OID_WWAN_MPDP 设置请求。
ms.assetid: 59B8D9A0-FB22-4252-A24B-A9E58B068C4E
keywords:
- NDIS_STATUS_WWAN_MPDP_STATE，从 Windows Vista 开始的网络驱动程序
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
ms.openlocfilehash: 2c6f108b5e38f10a2eda23ccfbfe31d715562592
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212813"
---
# <a name="ndis_status_wwan_mpdp_state"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE**通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个[OID_WWAN_MPDP](oid-wwan-mpdp.md)设置请求。

此通知不是作为未经请求的事件发送的。

此通知使用 [**NDIS_WWAN_MPDP_STATE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本1809

**标头**： Ndis。h