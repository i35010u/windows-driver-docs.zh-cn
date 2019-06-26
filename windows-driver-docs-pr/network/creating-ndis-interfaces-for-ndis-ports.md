---
title: 创建 NDIS 端口的 NDIS 接口
description: 创建 NDIS 端口的 NDIS 接口
ms.assetid: 3a856e4d-e32a-4c8a-8fa0-9976966bdf87
keywords:
- 端口 WDK NDIS，创建 NDIS 接口
- NDIS 端口 WDK，创建 NDIS 接口
- 注册 NDIS 接口提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8086afd731fe3c07aae924c0040f90e610a12d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374896"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>创建 NDIS 端口的 NDIS 接口





默认情况下，NDIS 不会创建 NDIS 端口的 NDIS 网络接口。 如果有必要，请 NDIS 驱动程序可以调用[ **NdisIfRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider)函数注册为 NDIS 接口提供程序并调用[ **NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)函数以注册一个端口的接口。

有关 NDIS 网络接口的详细信息，请参阅[NDIS 6.0 网络接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

 

 





