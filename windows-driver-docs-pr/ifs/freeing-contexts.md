---
title: 释放上下文
description: 释放上下文
keywords:
- 上下文 WDK 文件系统微筛选器，释放
- 释放上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7919dbdfc3dfd33e9090081a1b26ba028dec46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826855"
---
# <a name="freeing-contexts"></a>释放上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


上下文在被删除后会被释放，并且对它的所有未完成引用都已释放。

此规则有一个例外：如果已创建上下文但尚未通过调用 **FltSet**_Xxx_*_上下文_* 进行设置，则无需删除它。 它在其引用计数达到零时被释放。  (参见 [释放上下文](releasing-contexts.md)中的代码示例。 ) 

当微筛选器驱动程序注册其上下文类型时，每个上下文定义可以选择性地包含要在释放上下文之前调用的上下文清理回调例程。 有关详细信息，请参阅 [**PFLT \_ 上下文 \_ 清理 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)。

 

