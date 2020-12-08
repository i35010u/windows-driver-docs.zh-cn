---
title: NDIS_STATUS_WWAN_MPDP_LIST
description: NDIS_STATUS_WWAN_MPDP_LIST 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个 OID_WWAN_MPDP 查询请求。
keywords:
- NDIS_STATUS_WWAN_MPDP_LIST，从 Windows Vista 开始的网络驱动程序
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MPDP_LIST
api_location:
- ndis.h
api_type:
- HeaderDef
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1bb6ebaf5861baf19b1f56004bda43d4086083ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808057"
---
# <a name="ndis_status_wwan_mpdp_list"></a>NDIS_STATUS_WWAN_MPDP_LIST

**NDIS_STATUS_WWAN_MPDP_LIST** 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个 [OID_WWAN_MPDP](oid-wwan-mpdp.md)查询请求。

此通知不是作为未经请求的事件发送的。

此通知使用 [**NDIS_WWAN_MPDP_LIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本1809

**标头**： Ndis。h
