---
title: Bug 检查 0x90 PP1_INITIALIZATION_FAILED
description: PP1_INITIALIZATION_FAILED bug 检查的值为0x00000090。 此 bug 检查指示即插即用 (PnP) 管理器无法初始化。
keywords:
- Bug 检查 0x90 PP1_INITIALIZATION_FAILED
- PP1_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PP1_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06eef063405a05294a8fe5db1a05ea85cdbc13a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816417"
---
# <a name="bug-check-0x90-pp1_initialization_failed"></a>Bug 检查0x90： PP1 \_ 初始化 \_ 失败


PP1 \_ 初始化 \_ 失败 bug 检查的值为0x00000090。 此 bug 检查指示即插即用 (PnP) 管理器无法初始化。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pp1_initialization_failed-parameters"></a>PP1 \_ 初始化 \_ 失败参数


无

<a name="cause"></a>原因
-----

内核模式 PnP 管理器的阶段1初始化期间出错。

阶段1是大多数初始化完成的位置，包括设置注册表文件和其他环境设置，以便驱动程序在后续 i/o 初始化期间调用。

 

 




