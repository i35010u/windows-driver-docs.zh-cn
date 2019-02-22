---
title: 配置可选的微型端口驱动程序服务
description: 配置可选的微型端口驱动程序服务
ms.assetid: 42fe3863-ded0-4a02-9216-86fa4c167a49
keywords:
- 微型端口驱动程序 WDK 网络 （可选） 服务
- NDIS 微型端口驱动程序 WDK，可选的服务
- MiniportSetOptions
- 特征结构 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32acf87c53e965d4144c372286e886592680dd73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547496"
---
# <a name="configuring-optional-miniport-driver-services"></a>配置可选的微型端口驱动程序服务





NDIS 调用微型端口驱动程序[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数，以允许驱动程序以配置可选的服务。 NDIS 调用*MiniportSetOptions*微型端口驱动程序的调用的上下文中[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数。

*MiniportSetOptions*注册的默认入口点的可选*MiniportXxx*函数，而可以分配其他驱动程序资源。 若要注册可选*MiniportXxx*函数、 微型端口驱动程序调用[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数，并将传递在特征结构*OptionalHandlers*参数。

从 NDIS 6.0 开始，有效特征结构如下所示：

[**NDIS\_微型端口\_共同\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565948)

[**NDIS\_MINIPORT\_PNP\_CHARACTERISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff566475)

[**NDIS\_CO\_调用\_MANAGER\_可选\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff564883)

[**NDIS\_提供程序\_烟囱\_卸载\_泛型\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566846) (请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md))

[**NDIS\_提供程序\_烟囱\_卸载\_TCP\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566852) (请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md))

从开始 NDIS 6.30，有效特征结构还包括以下任务：

[**NDIS\_微型端口\_SS\_特征**](https://msdn.microsoft.com/library/windows/hardware/hh451559)

[**NDIS\_NDK\_PROVIDER\_CHARACTERISTICS**](https://msdn.microsoft.com/library/windows/hardware/hh451566)

 

 





