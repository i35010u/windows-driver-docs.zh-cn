---
title: 创建回调对象
description: 创建回调对象
ms.assetid: bbae1458-911f-4a48-8bf2-0997e8f98826
keywords:
- 回调对象 WDK UMDF
- 回调对象 WDK UMDF，创建
- 用户模式驱动程序框架 WDK 对象
- 用户模式驱动程序 WDK UMDF，对象
- UMDF 对象 WDK，回调对象
- framework 对象 WDK UMDF，回调对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18cf7083d053a77f280e5d3377342878fc962527
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358591"
---
# <a name="creating-callback-objects"></a>创建回调对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF 驱动程序可以创建*回调对象*，其中包含上下文数据和接口方法。 该框架通过驱动程序的回调接口方法来访问驱动程序的回调对象。

下图显示了如何驱动程序实现的回调对象对应于[framework 对象](framework-objects.md)。

![framework 对象和供应商提供的回调对象](images/correspond.gif)

UMDF 驱动程序可以创建多种类型的回调对象，其中包括：

-   驱动程序回调对象

    该框架使用驱动程序回调对象来初始化的驱动程序并通知到达的新设备驱动程序。

-   设备回调对象

    该驱动程序使用设备回调对象来存储设备上下文并处理清理和关闭文件对象和插 (PnP) 和电源管理 (PM) 事件。

-   队列回调对象

    驱动程序使用进程 i/o 队列回调对象。

下图显示了 UMDF 驱动程序如何创建设备回调对象。

![用于创建 umdf 设备回调对象调用序列](images/callback.gif)

以下主题包含代码示例演示如何创建回调对象：

-   [创建回调对象示例](creating-callback-objects-example.md)

-   [定义回调对象示例](defining-callback-objects-example.md)

-   [将相关联回调接口的示例](associating-callback-interfaces-example.md)

 

 





