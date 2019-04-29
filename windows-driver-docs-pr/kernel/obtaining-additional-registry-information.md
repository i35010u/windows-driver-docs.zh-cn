---
title: 获取其他注册表信息
description: 获取其他注册表信息
ms.assetid: 989acf63-3bb1-4d9a-a7a8-3eea1e2bc68a
keywords:
- 筛选注册表调用 WDK 内核，若要获取的其他信息
- 筛选驱动程序 WDK 内核，若要获取的其他信息的注册表
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa93162f0f9e189e34d63a2003b9fe8d0de15792
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382912"
---
# <a name="obtaining-additional-registry-information"></a>获取其他注册表信息


注册表筛选在 Windows Vista 和更高版本的操作系统版本运行的驱动程序可以获取有关注册表操作的以下附加信息：

-   对象标识符和名称

    [ **CmCallbackGetKeyObjectIDEx** ](https://msdn.microsoft.com/library/windows/hardware/jj215789)例程检索的注册表项的标识符和对象名称与指定的注册表密钥对象相关联。

-   事务对象

    [ **CmGetBoundTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff541905)例程返回一个指向该事务对象，表示[事务](using-kernel-transaction-manager.md)(如果有） 关联的注册表项对象。

-   版本信息

    [ **CmGetCallbackVersion** ](https://msdn.microsoft.com/library/windows/hardware/ff541912)例程检索有关配置管理器的注册表回调功能的最新版本的主版本号和次版本号。

 

 




