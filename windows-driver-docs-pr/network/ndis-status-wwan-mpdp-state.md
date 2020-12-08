---
title: NDIS_STATUS_WWAN_MPDP_STATE
description: NDIS_STATUS_WWAN_MPDP_STATE 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个 OID_WWAN_MPDP 设置请求。
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
ms.openlocfilehash: bbc691d03d31b5195e59e947081b50bd22d2cca2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822907"
---
# <a name="ndis_status_wwan_mpdp_state"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE** 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个 [OID_WWAN_MPDP](oid-wwan-mpdp.md)设置请求。

此通知不是作为未经请求的事件发送的。

此通知使用 [**NDIS_WWAN_MPDP_STATE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本1809

**标头**： Ndis。h
