---
title: NDIS_STATUS_WWAN_MPDP_LIST
description: 移动宽带的微型端口驱动程序发送 NDIS_STATUS_WWAN_MPDP_LIST 通知关于完成的上一个 OID_WWAN_MPDP 查询请求通知 MB 服务。
ms.assetid: 20D66ECE-A0F8-4902-BC91-3A3D385DA939
keywords:
- NDIS_STATUS_WWAN_MPDP_LIST，与 Windows Vista 一起启动的网络驱动程序
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
ms.openlocfilehash: e1ac1879c8ea04b76c8947aaf8f24ab03a9c6501
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569407"
---
# <a name="ndisstatuswwanmpdplist"></a>NDIS_STATUS_WWAN_MPDP_LIST

**NDIS_STATUS_WWAN_MPDP_LIST**移动宽带的微型端口驱动程序发送通知来告知在前一次完成 MB 服务[OID_WWAN_MPDP](oid-wwan-mpdp.md)查询请求。

为未经请求的事件不发送此通知。

使用此通知[ **NDIS_WWAN_MPDP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1809 |
| Header | Ndis.h |
