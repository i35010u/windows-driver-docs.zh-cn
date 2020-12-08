---
title: 获取当前的 WOL 模式设置
description: 获取当前的 WOL 模式设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88da3128870bb479410c55c1bb575945b7a10ee2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813669"
---
# <a name="obtaining-the-current-settings-of-wol-patterns"></a>获取当前的 WOL 模式设置





过量驱动程序可以使用 [oid \_ PM \_ WOL \_ 模式 \_ 列表](./oid-pm-wol-pattern-list.md) oid 查询请求来枚举基础网络适配器上设置的 LAN 唤醒 (WOL) 模式。 成功从查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含一个指针，该指针指向描述当前添加的 wol 模式的 [**NDIS \_ PM \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的列表。 有关 **NDIS \_ PM \_ WOL \_ 模式** 结构的内容的信息，请参阅 [添加和删除 LAN 唤醒模式](adding-and-deleting-wake-on-lan-patterns.md)。

NDIS 会 \_ \_ \_ \_ 代表微型端口驱动程序处理 oid PM WOL 模式列表 oid 请求。 因此，不需要 NDIS 微型端口驱动程序支持 OID \_ PM \_ WOL \_ 模式 \_ 列表 OID 请求。

 

