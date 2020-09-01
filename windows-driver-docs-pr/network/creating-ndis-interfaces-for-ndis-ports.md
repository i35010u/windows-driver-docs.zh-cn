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
ms.openlocfilehash: 6c73492023c3ee5bc87658bade0c5007c20f1b6e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210209"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>创建 NDIS 端口的 NDIS 接口





默认情况下，NDIS 不会为 NDIS 端口创建 NDIS 网络接口。 如有必要，NDIS 驱动程序可以调用 [**NdisIfRegisterProvider**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider) 函数以将其注册为 NDIS 接口提供程序，并调用 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数为端口注册接口。

有关 NDIS 网络接口的详细信息，请参阅 [ndis 6.0 网络接口](/windows-hardware/drivers/ddi/_netvista/)。

 

