---
title: Windows 内核模式对象管理器
description: Windows 内核模式对象管理器
ms.assetid: f10561a3-d831-4c13-9edf-be40fb1db403
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 984df7a548b7f2838ac86364410a5ba8cd82ad5a
ms.sourcegitcommit: f5222e608f2853003175244505d5daa3465ac6b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88615081"
---
# <a name="windows-kernel-mode-object-manager"></a>Windows 内核模式对象管理器


Windows 内核模式对象管理器组件管理 *对象*。 文件、设备、同步机制、注册表项等均表示为内核模式下的对象。 每个对象都有一个 *标头* (，其中包含有关对象的信息，如其名称、类型和位置) ，以及一个 *正文* (，其中包含由每种类型的对象) 确定的格式的数据。

Windows 有25多种类型的对象。 下面是几种类型：

-   文件

-   设备

-   线程数

-   进程

-   事件

-   Mutexes

-   信号量

-   注册表项

-   作业

-   部分

-   访问令牌

-   符号链接

对象管理器通过执行以下主要任务来管理 Windows 中的对象：

-   管理对象的创建和析构。

-   为跟踪对象信息保留对象命名空间数据库。

-   跟踪分配给每个进程的资源。

-   跟踪特定对象的访问权限以提供安全性。

-   管理对象的生存期，并确定何时将自动销毁对象以回收资源空间。

有关 Windows 中的对象的详细信息，请参阅 [管理内核对象](managing-kernel-objects.md)。

向对象管理器提供直接接口的例程通常以字母 "**Ob**" 作为前缀;例如， **ObGetObjectSecurity**。 有关对象管理器例程的列表，请参阅 [对象管理器例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557759(v=vs.85))。

请注意，Windows 使用对象作为资源的抽象。 但是，Windows 并不是面向对象的，它采用的是传统的 c + + 含义。 Windows 是 *基于对象*的。 有关 Windows 的基于对象的方法的详细信息，请参阅 [基于对象](object-based.md)。

 

 




