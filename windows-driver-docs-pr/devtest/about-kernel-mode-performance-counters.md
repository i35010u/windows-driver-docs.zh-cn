---
title: 内核模式下的性能计数器
description: 内核模式下的性能计数器
ms.assetid: 57655e65-6db4-487d-8831-282e8d30d84e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b134a6a302d30a5b7ea1912aae52cd44d20018f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533922"
---
# <a name="about-kernel-mode-performance-counters"></a>内核模式下的性能计数器


Windows 性能计数器 (PCW) 系统中与不同的组件进行交互，并用于跟踪的计数器集 （和其实例） 提供的内核模式组件。 此外，PCW 跟踪服务请求从使用者通过查看的计数器集，并返回所请求的数据。

内核模式 PCW 提供程序安装在系统中作为性能计数器库 (PERFLIB) （版本 2 提供程序），从而允许它们要浏览的计数器，并允许进行数据收集和实例的枚举。 使用者可以通过无需任何修改为使用者代码使用 PDH 和 PERFLIB 版本 1 查询 KM PCW 提供程序。 有关详细信息，请参阅[使用性能计数器进行开发](https://go.microsoft.com/fwlink/p/?linkid=144623)。

在内核模式下运行的提供程序通过使用内核模式 PCW 提供程序 API 来注册其计数器集。 提供程序可以管理已注册的计数器集的实例，并使用通知以了解与性能计数器相关的各种事件发生 （例如，当使用者添加、 删除或收集计数器）。

**请注意**  内核模式 PCW 提供程序 API （PERFLIB 版本 2），Windows 7 中引入当前不支持会话空间驱动程序。

 

 

 





