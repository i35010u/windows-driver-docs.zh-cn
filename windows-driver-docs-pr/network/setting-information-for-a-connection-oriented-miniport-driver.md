---
title: 设置面向连接的微型端口驱动程序的信息
description: 设置面向连接的微型端口驱动程序的信息
ms.assetid: e31d2054-5982-4ba5-a9e9-133c0d4ed875
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2868e950c1d4ed4f4a1234638189144cbad9ed5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563915"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>设置面向连接的微型端口驱动程序的信息





若要设置一个面向连接的微型端口驱动程序维护的 OID，绑定的协议调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711) ，并将传递[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，它指定的对象 (OID) 正被查询的和，它指向包含该对象应设置为值的缓冲区。 在调用**NdisCoOidRequest** NDIS 调用微型端口驱动程序将导致[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数，这将设置与所提供的值的对象。

在调用**NdisCoOidRequest**可以同步或异步完成。 若要以异步方式完成的调用，微型端口驱动程序调用[ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)。 下图演示了面向连接的微型端口驱动程序中的设置信息。

![说明面向连接的微型端口驱动程序中的设置信息的关系图](images/fig5-3.png)

 

 





