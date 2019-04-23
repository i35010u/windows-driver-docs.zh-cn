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
ms.openlocfilehash: 7a1942cc86cd92cee35373855ff746c9afc215d8
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902823"
---
# <a name="bug-check-0x90-pp1initializationfailed"></a>Bug 检查 0x90：PP1\_初始化\_失败


PP1\_初始化\_失败错误检查的值为 0x00000090。 此 bug 检查指示插即用 (PnP) 管理器无法初始化。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="pp1initializationfailed-parameters"></a>PP1\_初始化\_失败参数


无

<a name="cause"></a>原因
-----

第 1 阶段的内核模式即插即用管理器初始化期间出错。

阶段 1 是大部分初始化已完成，包括设置注册表文件和驱动程序的其他环境设置，若要在后续的 I/O 初始化期间调用。

 

 




