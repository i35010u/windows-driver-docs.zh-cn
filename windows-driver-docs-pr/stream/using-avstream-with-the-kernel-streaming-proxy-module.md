---
title: 将 AVStream 与内核流式处理代理模块配合使用
description: 将 AVStream 与内核流式处理代理模块配合使用
keywords:
- 内核流式处理代理 WDK AVStream
- KS 代理 WDK AVStream
- 代理用户模式连接 WDK AVStream
- 媒体类型 WDK AVStream
- DirectShow 筛选器 WDK AVStream
- AVStream 内核流式处理代理 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 653cb3673fb5889b6d13bcea11886dca2b3234af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795793"
---
# <a name="using-avstream-with-the-kernel-streaming-proxy-module"></a>将 AVStream 与内核流式处理代理模块配合使用





内核模式筛选器通常通过 [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index)在用户模式下进行连接。 此代理使内核模式筛选器作为 DirectShow 筛选器显示在用户模式下。

使用此连接模式时，DirectShow 会通过将筛选器与 *媒体类型* 交叉来连接这些筛选器。 这些媒体类型是内核模式下的数据格式的 DirectShow 对应项。

当 DirectShow 枚举内核模式 pin 上的媒体类型时，该 pin 上的相应数据范围与该 pin 的数据范围相交。 此交集产生数据格式，如 [AVStream 中的数据范围交集](data-range-intersections-in-avstream.md)中所述。 代理将生成的数据格式转换为 DirectShow 媒体类型。

与在内核模式中一样，代理会要求数据处理程序确定媒体类型是否可接受，或确定媒体类型是否是 pin 上数据范围的部分匹配项。 部分匹配指示在内核模式语义的上下文中，主要类型、subformat、说明符和所需属性匹配。 如果媒体类型是部分匹配，则连接将继续。

在连接完成之前，AVStream 会调用微型驱动程序的 [*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat) 调度，以通知微型驱动程序正在设置的数据格式。 此格式对应于已建议代理的 pin 的用户模式媒体类型。 AVStream 还提供已确定为该格式的部分匹配的数据范围。

 

