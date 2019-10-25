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
ms.openlocfilehash: fb710df30599f88697498b6214ee7538d1cb1a09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842099"
---
# <a name="registering-a-network-interface"></a>注册网络接口





当计算机重新启动时，NDIS 将从已注册的网络接口的空列表开始。 接口提供程序在启动或检测到接口并且其[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值已知时，将调用[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数。 用于启动或检测接口的机制是特定于应用程序的。

仅当 NDIS 成功将指定接口添加到其计算机上的已知接口列表中时， **NdisIfRegisterInterface**才会\_SUCCESS 返回 NDIS\_状态。 在这种情况下， **NdisIfRegisterInterface**将在*pIfIndex*参数处返回一个接口索引。 但是，对**NdisIfRegisterInterface**的调用并不意味着接口处于活动状态;此调用仅保证接口存在。 如果 NDIS 没有足够的资源可用于注册接口，则**NdisIfRegisterInterface**将返回 NDIS\_状态\_资源。 **NdisIfRegisterInterface**还可以返回其他 NDIS 状态值。

**NdisIfRegisterInterface**的*ProviderIfContext*参数包含调用方的接口上下文区域的句柄，此句柄传递给调用方的 OID 查询并设置函数。 [**如果\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_if_information)结构包含有关接口的信息，则*pIfInfo*参数包含指向 NET\_的指针。

以下主题提供了有关**NdisIfRegisterInterface**成功注册的网络接口的详细信息：

[分配接口索引](allocating-an-interface-index.md)

[网络接口信息](network-interface-information.md)

 

 





