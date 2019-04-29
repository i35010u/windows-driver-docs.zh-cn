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
ms.openlocfilehash: bb5c2189951c1fdc7c49c244c95df022f20c22ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364093"
---
# <a name="registering-as-an-interface-provider"></a>注册为接口提供程序





NDIS 接口提供程序是一个软件组件提供和管理的 NDIS 网络接口的信息。 例如，协议驱动程序、 MUX 中间驱动程序和 NDIS 是接口提供程序。 （NDIS 代理接口提供程序为提供微型端口驱动程序和筛选器驱动程序。 但是，微型端口驱动程序和筛选器驱动程序也可以是接口提供程序。）每个接口提供程序调用[ **NdisIfRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562716)函数注册为网络接口提供程序。

如果在调用**NdisIfRegisterProvider**成功， **NdisIfRegisterProvider**返回的地址上的句柄*pNdisProviderHandle*参数指定。 调用方在后续调用中 （例如，若要注册接口） 将使用此句柄。 *ProviderCharacteristics*参数指向[ **NDIS\_如果\_提供程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565728)结构包含提供程序的入口点来处理 OID 查询并将请求设置。 NDIS\_IF\_提供程序\_特征包括以下查询和设置的函数：

-   [**ProviderQueryObject**](https://msdn.microsoft.com/library/windows/hardware/ff570399)

-   [**ProviderSetObject**](https://msdn.microsoft.com/library/windows/hardware/ff570403)

详细了解接口提供程序查询和设置处理程序，请参阅[处理 OID 查询和 NDIS 接口提供程序中设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)。

NDIS 驱动程序可以调用[ **NdisIfDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562703)函数来为网络接口提供程序取消注册。 例如，NDIS 驱动程序应取消注册为接口提供程序时被卸载。 接口提供程序必须确保它没有注册，然后它会调用任何接口**NdisIfDeregisterProvider**。 提供程序必须使用在传递给它的提供程序句柄*NdisProviderHandle*的参数**NdisIfDeregisterProvider**它将调用后**NdisIfDeregisterProvider**.

 

 





