---
title: 与流式处理代理模块内核使用 AVStream
description: 与流式处理代理模块内核使用 AVStream
ms.assetid: c8ae1385-337e-46ad-841e-fbdf5d685210
keywords:
- 内核流式处理代理 WDK AVStream
- KS 代理 WDK AVStream
- 代理用户模式下连接 WDK AVStream
- 媒体类型 WDK AVStream
- DirectShow 筛选器 WDK AVStream
- AVStream 内核流式处理代理 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a99a391a0b448b68f2d1f86c0b4130776572b9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519519"
---
# <a name="using-avstream-with-the-kernel-streaming-proxy-module"></a>与流式处理代理模块内核使用 AVStream





内核模式下的筛选器通常连接在用户模式下通过[内核流式处理代理](https://msdn.microsoft.com/library/windows/hardware/ff560877)。 此代理在内核模式筛选器显示为作为 DirectShow 筛选器的用户模式。

使用这种模式的连接时，DirectShow 连接筛选器相交他们*媒体类型*。 这些媒体类型是在内核模式下的数据格式的 DirectShow 对应操作。

当 DirectShow 枚举的内核模式下插针的媒体类型时，相应的数据范围的插针相交时 pin 的数据范围。 此交集生成的数据格式，如中所述[AVStream 中的数据范围交集](data-range-intersections-in-avstream.md)。 代理将 DirectShow 媒体类型转换为生成的数据格式。

如下所示内核模式下，代理也会要求数据处理程序以确定是否的媒体类型是可接受的或者它确定媒体类型是否为数据范围的插针的部分匹配项。 部分匹配的内核模式的语义、 主要类型、 子格式、 说明符，上下文中指示的并且必需的属性匹配。 如果媒体类型是部分匹配，将继续连接。

AVStream 连接完毕之前，调用微型驱动程序的[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)调度通知设置的数据格式的微型驱动程序。 这种格式对应于已建议为代理的 pin 的用户模式下媒体类型。 AVStream 还提供了已确定是部分匹配项的格式的数据范围。

 

 




