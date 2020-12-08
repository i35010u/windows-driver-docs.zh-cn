---
title: 中继器
description: 中继器
keywords:
- 通过中继器进行远程调试
- repeater
- 中继器，概述
- DbEngPrx
- DbEngPrx，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74cb9cd01cdfe2914e4aa23a3ebe1194e086128a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816935"
---
# <a name="repeaters"></a>中继器


## <span id="ddk_repeaters_dbg"></span><span id="DDK_REPEATERS_DBG"></span>


*中继器* 是在计算机上运行并在其他两台计算机之间中继数据的轻型代理服务器。 中继器不会以任何方式处理数据。 其他两台计算机几乎会注意到中继器;从其角度看，这似乎是直接连接到对方。

在这两台计算机上运行的进程称为 *服务器* 和 *客户端*。 它们与中继器的观点之间没有任何根本区别，只不过在大多数情况下，服务器首先启动，然后是中继器，最后是客户端。

适用于 Windows 的调试工具包中包含一个名为 DbEngPrx 的中继器 ( # A0) 。

本节包括：

[**激活中继器**](activating-a-repeater.md)

[使用中继器](using-a-repeater.md)

[中继器示例](repeater-examples.md)

 

 





