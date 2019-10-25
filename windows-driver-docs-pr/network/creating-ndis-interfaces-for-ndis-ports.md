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
ms.openlocfilehash: be7d5fb1b2228a7f29dd3c36e7af931451943745
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835021"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>创建 NDIS 端口的 NDIS 接口





默认情况下，NDIS 不会为 NDIS 端口创建 NDIS 网络接口。 如有必要，NDIS 驱动程序可以调用[**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)函数以将其注册为 NDIS 接口提供程序，并调用[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数为端口注册接口。

有关 NDIS 网络接口的详细信息，请参阅[ndis 6.0 网络接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 





