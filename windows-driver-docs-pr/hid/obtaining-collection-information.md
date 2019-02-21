---
title: 获取集合的信息
description: 获取集合的信息
ms.assetid: 0568993b-ff50-48ac-a875-95ab643d6c28
keywords:
- WDK HID，收集的信息的集合
- HID 的集合 WDK，收集的信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 871aa3a668e7554dbb7002a313d2963c67067b60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521150"
---
# <a name="obtaining-collection-information"></a>获取集合的信息





本部分讲述获取用户模式应用程序和内核模式驱动程序使用来操作的信息[HID 集合](hid-collections.md)。

将应用程序或驱动程序已连接到 HID 集合后，它可以获取以下信息：

-   [集合的功能](collection-capability.md)。

-   [按钮功能数组](button-capability-arrays.md)并[值功能数组](value-capability-arrays.md)，其中描述的按钮和值集合支持的功能。

-   说明如何组织内部的链接集合数组及其[将集合链接](link-collections.md)。

此信息包括[HID 用法](hid-usages.md)的集合和集合支持的所有控件。 如果应用程序或驱动程序不使用这些控件，它应立即关闭其连接到的集合。

获取此信息后, 的应用程序或驱动程序具有所需访问 HID 报表中的控件数据的信息。

 

 




