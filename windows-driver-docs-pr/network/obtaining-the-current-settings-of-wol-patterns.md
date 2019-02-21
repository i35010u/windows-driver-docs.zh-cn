---
title: 获取当前设置的 WOL 模式
description: 获取当前设置的 WOL 模式
ms.assetid: 113ea75a-83d8-41aa-b61c-711ef90bccca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea292475114e3a8d5e21eca322fb7f02c8e7bb96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523486"
---
# <a name="obtaining-the-current-settings-of-wol-patterns"></a>获取当前设置的 WOL 模式





过量驱动程序可以使用[OID\_PM\_WOL\_模式\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569772)OID 查询请求要枚举的基础的网络适配器设置的 LAN 唤醒 (WOL) 模式。 从查询中，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指针到一系列[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)描述了当前添加了各种 WOL 模式的结构。 有关的内容信息**NDIS\_PM\_WOL\_模式**结构，请参阅[添加和删除唤醒 LAN 模式](adding-and-deleting-wake-on-lan-patterns.md)。

NDIS 处理 OID\_PM\_WOL\_模式\_代表微型端口驱动程序请求列表 OID。 因此，NDIS 微型端口驱动程序不支持所需 OID\_PM\_WOL\_模式\_列表 OID 请求。

 

 





