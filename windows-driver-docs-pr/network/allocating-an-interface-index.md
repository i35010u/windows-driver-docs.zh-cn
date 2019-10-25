---
title: 分配接口索引
description: 分配接口索引
ms.assetid: f1315da2-16da-4320-9d0d-1270396af38b
keywords:
- NDIS 网络接口 WDK，接口索引分配
- 网络接口 WDK，接口索引分配
- 接口索引 WDK 网络
- 正在分配网络接口索引
- 索引操作 WDK 网络接口
- 本地唯一标识符 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e887742f5099b0e7192245a31b0af376ef0803a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835368"
---
# <a name="allocating-an-interface-index"></a>分配接口索引





如果接口提供程序通过调用[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数成功注册接口，NDIS 将为该接口分配一个接口索引，并返回*pIfIndex*参数说明. 接口索引是在本地计算机上唯一的16位值。 在计算机重新启动后，如果接口提供程序注册了相同的[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)值，NDIS 不保证它将分配相同的接口索引。 接口索引值零（NET\_IFINDEX\_未指定）是保留的，NDIS 不会将其分配给任何接口。

 

 





