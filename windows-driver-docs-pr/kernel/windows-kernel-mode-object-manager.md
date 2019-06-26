---
title: Windows 内核模式对象管理器
description: Windows 内核模式对象管理器
ms.assetid: f10561a3-d831-4c13-9edf-be40fb1db403
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d27c51d02b3c7ad393278f14170782cdc772c766
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374172"
---
# <a name="windows-kernel-mode-object-manager"></a>Windows 内核模式对象管理器


Windows 内核模式对象管理器组件管理*对象*。 文件、 设备、 的同步机制、 注册表项和等等，都表示为在内核模式下的对象。 每个对象都*标头*（包含有关其名称、 类型和位置等对象的信息），和一个*正文*（包含数据格式由每种类型的对象）。

Windows 具有 25 个以上类型的对象。 几个类型是：

-   文件

-   设备

-   线程

-   进程

-   Events

-   互斥锁

-   信号量

-   注册表项

-   作业

-   部分

-   访问令牌

-   符号链接

对象管理器管理 Windows 中的对象执行以下主要任务：

-   管理创建和销毁的对象。

-   保留用于跟踪的对象信息的对象命名空间数据库。

-   持续跟踪的资源分配给每个进程。

-   跟踪的特定对象提供安全的访问权限。

-   管理对象的生存期，并确定当销毁的对象将自动回收资源空间。

有关在 Windows 中的对象的详细信息，请参阅[设备对象和设备堆栈](device-objects-and-device-stacks.md)。

向对象管理器提供直接接口的例程都通常带有前缀字母"**Ob**"; 例如， **ObGetObjectSecurity**。 对象管理器例程的列表，请参阅[对象管理器例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557759(v=vs.85))。

请注意，Windows 使用对象作为一种抽象的资源。 但是，Windows 不是面向对象的在传统C++一词的含义。 Windows 是*基于对象的*。 Windows 基于对象的含义的更多信息，请参阅[基于对象的](object-based.md)。

 

 




