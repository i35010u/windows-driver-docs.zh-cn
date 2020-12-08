---
title: 获取其他注册表信息
description: 获取其他注册表信息
keywords:
- 筛选注册表调用 WDK 内核，获取其他信息
- 注册表筛选驱动程序 WDK 内核，要获取的其他信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed5df05c5649dd14a50bf3fc5a41a44688e8e29d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788625"
---
# <a name="obtaining-additional-registry-information"></a>获取其他注册表信息


在 Windows Vista 及更高版本的操作系统上运行的注册表筛选驱动程序可以获取以下有关注册表操作的其他信息：

-   对象标识符和名称

    [**CmCallbackGetKeyObjectIDEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmcallbackgetkeyobjectidex)例程检索与指定的注册表项对象相关联的注册表项标识符和对象名。

-   事务对象

    [**CmGetBoundTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetboundtransaction)例程返回指向 transaction 对象的指针，该对象表示与某个注册表项对象关联的 [事务](introduction-to-ktm.md)（如果有）。

-   版本信息

    [**CmGetCallbackVersion**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetcallbackversion)例程检索当前版本的 configuration manager 的注册表回调功能的主要版本号和次版本号。

 

