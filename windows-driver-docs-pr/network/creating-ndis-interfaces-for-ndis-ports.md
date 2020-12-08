---
title: 创建 NDIS 端口的 NDIS 接口
description: 创建 NDIS 端口的 NDIS 接口
keywords:
- 端口 WDK NDIS，创建 NDIS 接口
- NDIS 端口 WDK，创建 NDIS 接口
- 注册 NDIS 接口提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209ed83c943adf24b85256e203c40cfde76cd62e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794657"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>创建 NDIS 端口的 NDIS 接口





默认情况下，NDIS 不会为 NDIS 端口创建 NDIS 网络接口。 如有必要，NDIS 驱动程序可以调用 [**NdisIfRegisterProvider**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider) 函数以将其注册为 NDIS 接口提供程序，并调用 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数为端口注册接口。

有关 NDIS 网络接口的详细信息，请参阅 [ndis 6.0 网络接口](/windows-hardware/drivers/ddi/_netvista/)。

 

