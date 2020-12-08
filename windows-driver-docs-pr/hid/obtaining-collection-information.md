---
title: 获取集合信息
description: 获取集合信息
keywords:
- 集合 WDK HID，信息收集
- HID 集合 WDK，信息收集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60dc7e4aa47e53cc6e5f5f4a15d0aef922ac349
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805603"
---
# <a name="obtaining-collection-information"></a>获取集合信息





本部分介绍用户模式的应用程序和内核模式驱动程序用来操作 [HID 集合](hid-collections.md)的信息。

在应用程序或驱动程序连接到 HID 集合后，它可以获取以下信息：

-   [集合的功能](collection-capability.md)。

-   [按钮功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md)，用于描述集合支持的按钮和值的功能。

-   链接集合数组，描述其 [链接集合](link-collections.md)的内部组织。

此信息包括集合和集合支持的所有控件的 [HID 使用情况](hid-usages.md) 。 如果应用程序或驱动程序不使用这些控件，它应立即关闭与集合的连接。

获取此信息后，应用程序或驱动程序具有访问 HID 报表中的控件数据所需的信息。

 

 




