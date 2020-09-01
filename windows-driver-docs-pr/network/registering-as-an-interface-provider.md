---
title: 注册为接口提供程序
description: 注册为接口提供程序
ms.assetid: 7eb4b86d-077a-48de-94b6-11906e847569
keywords:
- NDIS 网络接口 WDK，接口提供程序
- 网络接口 WDK，接口提供程序
- 接口提供程序 WDk 网络接口
- 注册接口提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06beb50d528641c1b86433fab5dae38120191449
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213167"
---
# <a name="registering-as-an-interface-provider"></a>注册为接口提供程序





NDIS 接口提供程序是一个软件组件，用于提供和管理 NDIS 网络接口的信息。 例如，协议驱动程序、MUX 中间驱动程序和 NDIS 都是接口提供程序。  (NDIS 为微型端口驱动程序和筛选器驱动程序提供代理接口提供程序。 但是，微型端口驱动程序和筛选器驱动程序也可以是接口提供程序。 ) 每个接口提供程序调用 [**NdisIfRegisterProvider**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider) 函数以注册为网络接口提供程序。

如果对 **NdisIfRegisterProvider** 的调用成功，则 **NdisIfRegisterProvider** 将返回 *pNdisProviderHandle* 参数指定的地址处的句柄。 调用方在后续调用中使用此句柄 (例如，将接口注册) 。 [** \_ 如果 \_ 提供 \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_if_provider_characteristics)程序的入口点包含用于处理 OID 查询和设置请求的提供程序入口点，则*ProviderCharacteristics*参数指向 NDIS。 \_如果 \_ 提供程序 \_ 特征包含以下查询并设置函数，则设置 NDIS：

-   [**ProviderQueryObject**](/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)

-   [**ProviderSetObject**](/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object)

有关接口提供程序查询和设置处理程序的详细信息，请参阅 [在 NDIS 接口提供程序中处理 OID 查询和设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)。

NDIS 驱动程序可以调用 [**NdisIfDeregisterProvider**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider) 函数以取消注册为网络接口提供程序。 例如，当卸载 NDIS 驱动程序时，应将其作为接口提供程序取消注册。 在调用 **NdisIfDeregisterProvider**之前，接口提供程序必须确保未注册任何接口。 提供程序在调用**NdisIfDeregisterProvider**后，不能使用它在**NdisIfDeregisterProvider**的*NdisProviderHandle*参数传递的提供程序句柄。

 

