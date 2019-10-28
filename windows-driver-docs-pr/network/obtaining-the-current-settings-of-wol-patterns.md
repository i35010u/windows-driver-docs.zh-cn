---
title: 获取当前的 WOL 模式设置
description: 获取当前的 WOL 模式设置
ms.assetid: 113ea75a-83d8-41aa-b61c-711ef90bccca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b83554a74910baa8935810cdc5cb757687026074
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837740"
---
# <a name="obtaining-the-current-settings-of-wol-patterns"></a>获取当前的 WOL 模式设置





过量驱动程序可以使用[OID\_PM\_WOL\_模式\_列出](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-wol-pattern-list)oid 查询请求来枚举基础网络适配器上设置的 LAN 唤醒（WOL）模式。 成功从查询返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**ndis\_PM 列表的指针\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构，用于描述当前添加的 WOL 模式。 有关 NDIS\_PM 的内容的信息 **\_WOL\_模式**结构，请参阅[添加和删除 LAN 唤醒模式](adding-and-deleting-wake-on-lan-patterns.md)。

NDIS 处理 OID\_PM\_WOL\_模式，\_代表微型端口驱动程序列出 OID 请求。 因此，不需要 NDIS 微型端口驱动程序支持 OID\_PM\_WOL\_模式\_列表 OID 请求。

 

 





