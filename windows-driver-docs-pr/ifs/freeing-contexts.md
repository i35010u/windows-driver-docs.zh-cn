---
title: 释放上下文
description: 释放上下文
ms.assetid: e2b87662-c1bd-45a7-82a3-29817f7692fc
keywords:
- 上下文 WDK 文件系统微筛选器，释放
- 释放上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35de4abf1c31ffb1043125ad53a25f09b9b3167f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063610"
---
# <a name="freeing-contexts"></a>释放上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


上下文在被删除后会被释放，并且对它的所有未完成引用都已释放。

此规则有一个例外：如果已创建上下文但尚未通过调用 **FltSet***Xxx***上下文**进行设置，则无需删除它。 它在其引用计数达到零时被释放。  (参见 [释放上下文](releasing-contexts.md)中的代码示例。 ) 

当微筛选器驱动程序注册其上下文类型时，每个上下文定义可以选择性地包含要在释放上下文之前调用的上下文清理回调例程。 有关详细信息，请参阅 [**PFLT \_ 上下文 \_ 清理 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)。

 

