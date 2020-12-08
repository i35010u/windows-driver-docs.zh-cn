---
title: AVStream 中的互斥
description: AVStream 中的互斥
keywords:
- AVStream mutex WDK
- mutex WDK AVStream
- 对象 WDK AVStream
- 层次结构 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab350181c256ef930e512db0d7b867d6eb137850
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795275"
---
# <a name="mutexes-in-avstream"></a>AVStream 中的互斥





AVStream 微型驱动程序使用互斥体和进程控制入口同步对对象的访问。 有关过程控制入口的详细信息，请参阅 [AVStream 中的流控制入口](flow-control-gates-in-avstream.md)。

AVStream 具有三个不同的互斥体，微型驱动程序可以直接访问这些互斥体：

[AVStream 中的设备互斥](device-mutex-in-avstream.md)

[AVStream 中的筛选器控件互斥](filter-control-mutex-in-avstream.md)

[在 AVStream 中处理互斥](processing-mutex-in-avstream.md)

使用设备 mutex 将设备中的层次结构对象同步到筛选器。 使用筛选器控件互斥体将对象从筛选器同步到 pin。

多个 AVStream API 函数要求持有特定的 mutex。 相关函数引用页状态（如果在调用该特定函数时应持有特定互斥体）。

 

 




