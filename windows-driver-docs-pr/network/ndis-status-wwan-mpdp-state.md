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
ms.openlocfilehash: 8004b4d1d8e1f5387d99a824f701d0172472f38d
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968534"
---
# <a name="ndis_status_wwan_mpdp_state"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE**通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个[OID_WWAN_MPDP](oid-wwan-mpdp.md)设置请求。

此通知不是作为未经请求的事件发送的。

此通知使用[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本1809

**标头**： Ndis。h

