---
title: 关于内核模式性能计数器
description: 关于内核模式性能计数器
ms.assetid: 57655e65-6db4-487d-8831-282e8d30d84e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80fce5d09c2d60eaa2432de0a89d5eb2f2d74990
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769421"
---
# <a name="about-kernel-mode-performance-counters"></a>关于内核模式性能计数器


Windows 性能计数器（PCW）与系统中的不同组件进行交互，并跟踪内核模式组件提供的计数器集（及其实例）。 此外，PCW 通过检查计数器集并返回所请求的数据，来跟踪使用者的服务请求。

内核模式 PCW 提供程序在系统中安装为性能计数器库（PERFLIB）（版本2提供程序），这允许浏览其计数器，并允许数据收集和实例枚举。 使用者无需修改使用者代码即可使用 PDH 和 PERFLIB 版本1查询 KM PCW 提供程序。 有关详细信息，请参阅 [性能计时器](https://docs.microsoft.com/windows/win32/perfctrs/performance-counters-portal)。

在内核模式下运行的提供程序通过使用内核模式 PCW 提供程序 API 来注册其计数器集。 提供程序可以管理已注册计数器集的实例，并在发生与性能计数器相关的各种事件时（例如，使用者添加、删除或收集计数器时）通知通知。

**注意**   Windows 7 中引入的内核模式 PCW 提供程序 API （PERFLIB 版本2）目前不支持会话空间驱动程序。

 

 

 





