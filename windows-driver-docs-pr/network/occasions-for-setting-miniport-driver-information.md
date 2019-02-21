---
title: 有关设置微型端口驱动程序信息的情况下
description: 有关设置微型端口驱动程序信息的情况下
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b0ef7ce7e8709f3171c922bc57fff1fbc6e08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544511"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>有关设置微型端口驱动程序信息的情况下





[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)无连接的微型端口驱动程序中的函数和[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)中的函数在初始化期间调用的面向连接的微型端口驱动程序。 也可以调用这些函数：

-   在硬件重置，过程

-   如果协议调用[ **NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)。

*MiniportOidRequest*或*MiniportCoOidRequest*期间调用[硬件重置操作](hardware-reset.md)。 在这种情况下， *MiniportOidRequest*或*MiniportCoOidRequest*调用重置为其初始状态相对于其地址的微型端口驱动程序。

NDIS 调用*MiniportOidRequest*或*MiniportCoOidRequest*的协议时关闭微型端口驱动程序的 NIC [ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)调用。 这样的微型端口驱动程序将请求来更新其寻址信息。

 

 





