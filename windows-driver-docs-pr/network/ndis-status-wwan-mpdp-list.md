---
title: NDIS_STATUS_WWAN_MPDP_LIST
description: NDIS_STATUS_WWAN_MPDP_LIST 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了以前的 OID_WWAN_MPDP 查询请求。
ms.assetid: 20D66ECE-A0F8-4902-BC91-3A3D385DA939
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
ms.openlocfilehash: 12f5e9b451c01db66b4e2a6c404704e4c1a28012
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838888"
---
# <a name="ndis_status_wwan_mpdp_list"></a>NDIS_STATUS_WWAN_MPDP_LIST

**NDIS_STATUS_WWAN_MPDP_LIST**通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了以前的[OID_WWAN_MPDP](oid-wwan-mpdp.md)查询请求。

此通知不是作为未经请求的事件发送的。

此通知使用[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1809 |
| 标头 | Ndis。h |
