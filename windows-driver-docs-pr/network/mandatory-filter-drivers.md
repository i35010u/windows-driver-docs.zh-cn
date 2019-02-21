---
title: 必需的筛选器驱动程序
description: 必需的筛选器驱动程序
ms.assetid: 7be7cb9d-d0a6-4d4b-9dc1-2fef73b1f10e
keywords:
- 筛选器驱动程序 WDK 网络必需
- NDIS 筛选器驱动程序 WDK，必需
- 必需的筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ce74c70686c5ebca0d4b53c7940c44a281eefe0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519582"
---
# <a name="mandatory-filter-drivers"></a>必需的筛选器驱动程序





必需的筛选器驱动程序是必须存在才能正常运行的驱动程序堆栈的筛选器驱动程序。 如果未附加的必需的筛选器模块，将销毁驱动程序堆栈的其余部分。 [修改或监视筛选器驱动程序](types-of-filter-drivers.md)可以是强制性。 所有筛选器中间驱动程序是可选的。

若要将必需的筛选器模块附加到驱动程序堆栈，NDIS 取消绑定所有协议绑定，将附加筛选器模块，然后重新建立所有协议绑定。 如果未附加驱动程序，NDIS 消除基础驱动程序堆栈。

若要分离的驱动程序堆栈提供必需的筛选器的模块，NDIS，取消绑定所有协议绑定分离筛选器模块，然后重新建立协议绑定。 若要分离的可选筛选器模块，NDIS 暂停堆栈，并会在不取消绑定协议驱动程序的情况下重启它。

在计算机重新启动时，NDIS 不会绑定任何协议驱动程序到微型端口适配器如果与适配器相关联的任何必需的筛选器模块不会附加到的微型端口适配器。

若要安装必需的筛选器驱动程序，必须指定值为 0x00000001 **FilterRunType** INF 文件中。 若要安装的可选筛选器驱动程序，必须指定一个值为 0x00000002 **FilterRunType** INF 文件中。

 

 





