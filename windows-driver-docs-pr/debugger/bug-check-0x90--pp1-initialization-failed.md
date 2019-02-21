---
title: Bug 检查 0x90 PP1_INITIALIZATION_FAILED
description: PP1_INITIALIZATION_FAILED bug 检查具有 0x00000090 值。 此 bug 检查指示插即用 (PnP) 管理器无法初始化。
ms.assetid: 8dd46d24-0174-4310-953e-7b451ae34c71
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
ms.openlocfilehash: dccd648aaac85477a8644719a2492899369cb5d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521635"
---
# <a name="bug-check-0x90-pp1initializationfailed"></a>Bug 检查 0x90:PP1\_初始化\_失败


PP1\_初始化\_失败错误检查的值为 0x00000090。 此 bug 检查指示插即用 (PnP) 管理器无法初始化。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="pp1initializationfailed-parameters"></a>PP1\_初始化\_失败参数


无

<a name="cause"></a>原因
-----

第 1 阶段的内核模式即插即用管理器初始化期间出错。

阶段 1 是大部分初始化已完成，包括设置注册表文件和驱动程序的其他环境设置，若要在后续的 I/O 初始化期间调用。

 

 




