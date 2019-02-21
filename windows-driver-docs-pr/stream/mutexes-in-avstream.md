---
title: 在 AVStream Mutex
description: 在 AVStream Mutex
ms.assetid: 011edaaa-7449-41c3-8cfb-0d319901af8b
keywords:
- AVStream 互斥体 WDK
- 互斥体，WDK AVStream
- WDK AVStream 对象
- 层次结构 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65dda3311d6ffbc40dedd06e6d1b396e1b79cde5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533656"
---
# <a name="mutexes-in-avstream"></a>在 AVStream Mutex





AVStream 微型驱动程序通过使用互斥锁和过程控制门同步访问对象。 有关过程控制门的详细信息，请参阅[AVStream 在流控制门](flow-control-gates-in-avstream.md)。

AVStream 具有三个不同的 mutex，所有这些都是直接访问的微型驱动程序：

[设备在 AVStream 的互斥体](device-mutex-in-avstream.md)

[筛选器控件中 AVStream 的互斥体](filter-control-mutex-in-avstream.md)

[处理在 AVStream 互斥体](processing-mutex-in-avstream.md)

使用设备互斥体同步设备以筛选从层次结构对象。 使用筛选器控件互斥体同步中筛选器以固定的对象。

多个 AVStream API 函数需要保留该特定的互斥体。 相关函数引用页状态如果调用该特定函数时，应保留特定的互斥体。

 

 




