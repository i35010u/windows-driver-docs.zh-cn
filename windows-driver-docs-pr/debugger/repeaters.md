---
title: 中继器
description: 中继器
ms.assetid: 10f4f033-f6c1-4b4f-a35f-eadb4e15686d
keywords:
- 远程调试通过 repeater
- repeater
- repeater 概述
- DbEngPrx
- DbEngPrx 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f8f49369db782d1995d3e2cf92b3a077827add8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382078"
---
# <a name="repeaters"></a>中继器


## <span id="ddk_repeaters_dbg"></span><span id="DDK_REPEATERS_DBG"></span>


一个*repeater*是轻型代理服务器的计算机上运行并中继两台其他计算机之间的数据。 Repeater 不处理任何方式中的数据。 两台计算机几乎不能注意到 repeater;从其角度来看看起来是像直接连接到对方。

这两台其他计算机上运行的进程称为*服务器*并*客户端*。 没有任何从 repeater 的角度来看，它们之间的根本区别，但在大多数情况下在服务器启动第一个，则 repeater，和最后的客户端。

有关 Windows 调试工具包中包含名为 DbEngPrx (dbengprx.exe) repeater。

本部分包括：

[**激活 Repeater**](activating-a-repeater.md)

[使用 Repeater](using-a-repeater.md)

[Repeater 示例](repeater-examples.md)

 

 





