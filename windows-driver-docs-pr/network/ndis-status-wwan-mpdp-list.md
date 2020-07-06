---
title: NDIS_STATUS_WWAN_MPDP_LIST
description: NDIS_STATUS_WWAN_MPDP_LIST 通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个 OID_WWAN_MPDP 查询请求。
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
ms.openlocfilehash: 86cb9b504af43af2384dacfb9025053465b31f85
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968538"
---
# <a name="ndis_status_wwan_mpdp_list"></a>NDIS_STATUS_WWAN_MPDP_LIST

**NDIS_STATUS_WWAN_MPDP_LIST**通知由移动宽带微型端口驱动程序发送，通知 MB 服务完成了上一个[OID_WWAN_MPDP](oid-wwan-mpdp.md)查询请求。

此通知不是作为未经请求的事件发送的。

此通知使用[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本1809

**标头**： Ndis。h

