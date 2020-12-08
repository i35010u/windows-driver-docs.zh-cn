---
title: 必需的筛选器驱动程序
description: 必需的筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 网络，必需
- NDIS 筛选器驱动程序 WDK，必需
- 必需筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3089954635e0f322760c322e35137724d6622a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833365"
---
# <a name="mandatory-filter-drivers"></a>必需的筛选器驱动程序





必需筛选器驱动程序是驱动程序堆栈正常运行所必须存在的筛选器驱动程序。 如果未附加必需的筛选器模块，则驱动程序堆栈的其余部分将被破坏。 [修改或监视筛选器驱动程序](types-of-filter-drivers.md) 可能是必需的。 所有筛选器中间驱动程序都是可选的。

若要将强制筛选器模块附加到驱动程序堆栈，NDIS 将解除所有协议绑定的绑定，附加筛选器模块，然后重建所有协议绑定。 如果驱动程序未附加，NDIS 泪水基础驱动程序堆栈。

若要从驱动程序堆栈分离强制筛选器模块，NDIS 将所有协议绑定分离出筛选器模块，然后重建协议绑定。 若要分离可选筛选器模块，NDIS 将暂停堆栈并重新启动，而不会解除协议驱动程序绑定。

当计算机重新启动时，如果与适配器关联的任何必需的筛选器模块不会附加到微型端口适配器，NDIS 不会将任何协议驱动程序绑定到微型端口适配器。

若要安装必需的筛选器驱动程序，必须在 INF 文件中将 **FilterRunType** 的值指定为0x00000001。 若要安装可选筛选器驱动程序，必须在 INF 文件中为 **FilterRunType** 指定值0x00000002。

 

 





