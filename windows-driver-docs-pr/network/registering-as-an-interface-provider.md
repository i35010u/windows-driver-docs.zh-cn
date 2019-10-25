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
ms.openlocfilehash: 9e2c8281920f82345770ecb368206308d1f131c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842085"
---
# <a name="registering-as-an-interface-provider"></a>注册为接口提供程序





NDIS 接口提供程序是一个软件组件，用于提供和管理 NDIS 网络接口的信息。 例如，协议驱动程序、MUX 中间驱动程序和 NDIS 都是接口提供程序。 （NDIS 为微型端口驱动程序和筛选器驱动程序提供代理接口提供程序。 但是，微型端口驱动程序和筛选器驱动程序也可以是接口提供程序。）每个接口提供程序调用[**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)函数以注册为网络接口提供程序。

如果对**NdisIfRegisterProvider**的调用成功，则**NdisIfRegisterProvider**将返回*pNdisProviderHandle*参数指定的地址处的句柄。 调用方在后续调用中使用此句柄（例如，注册接口）。 [**如果\_提供程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_if_provider_characteristics)结构包含提供程序用于处理 OID 查询和设置请求的入口点，则*ProviderCharacteristics*参数指向 NDIS\_。 如果\_提供程序\_特征包含以下查询并设置函数，则 NDIS\_：

-   [**ProviderQueryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)

-   [**ProviderSetObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object)

有关接口提供程序查询和设置处理程序的详细信息，请参阅[在 NDIS 接口提供程序中处理 OID 查询和设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)。

NDIS 驱动程序可以调用[**NdisIfDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider)函数以取消注册为网络接口提供程序。 例如，当卸载 NDIS 驱动程序时，应将其作为接口提供程序取消注册。 在调用**NdisIfDeregisterProvider**之前，接口提供程序必须确保未注册任何接口。 提供程序在调用**NdisIfDeregisterProvider**后，不能使用它在**NdisIfDeregisterProvider**的*NdisProviderHandle*参数传递的提供程序句柄。

 

 





