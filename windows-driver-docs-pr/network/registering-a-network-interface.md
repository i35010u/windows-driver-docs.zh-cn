---
title: 注册网络接口
description: 注册网络接口
ms.assetid: 7e3c3b0f-2013-4133-8b52-fa9e66f963cb
keywords:
- NDIS 网络接口 WDK，注册
- 网络接口 WDK，注册
- 正在注册网络接口
- NdisIfRegisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5f80e0a3c803b38e27c20aeaee182331439cdb7
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715886"
---
# <a name="registering-a-network-interface"></a>注册网络接口





当计算机重新启动时，NDIS 将从已注册的网络接口的空列表开始。 接口提供程序在启动或检测到接口时，将调用 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数，并且它的 [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 值是已知的。 用于启动或检测接口的机制是特定于应用程序的。

**NdisIfRegisterInterface** \_ \_ 仅当 ndis 将指定接口成功添加到计算机上的已知接口列表中时，NDISIFREGISTERINTERFACE 才会返回 ndis 状态成功。 在这种情况下， **NdisIfRegisterInterface** 将在 *pIfIndex* 参数处返回一个接口索引。 但是，对 **NdisIfRegisterInterface** 的调用并不意味着接口处于活动状态;此调用仅保证接口存在。 **NdisIfRegisterInterface** \_ \_ 如果 ndis 没有足够的资源可用于注册接口，则 NdisIfRegisterInterface 将返回 ndis 状态资源。 **NdisIfRegisterInterface** 还可以返回其他 NDIS 状态值。

**NdisIfRegisterInterface**的*ProviderIfContext*参数包含调用方的接口上下文区域的句柄，此句柄传递给调用方的 OID 查询并设置函数。 *PIfInfo*参数包含指向包含接口相关信息的[**NET \_ IF \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_if_information)结构的指针。

以下主题提供了有关 **NdisIfRegisterInterface** 成功注册的网络接口的详细信息：

[分配接口索引](allocating-an-interface-index.md)

[网络接口信息](network-interface-information.md)

 

