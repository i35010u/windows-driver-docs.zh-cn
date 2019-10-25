---
title: 释放上下文
description: 释放上下文
ms.assetid: e2b87662-c1bd-45a7-82a3-29817f7692fc
keywords:
- 上下文 WDK 文件系统微筛选器，释放
- 释放上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8130c31ee714110e6398f70b004706472ff6ee3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841331"
---
# <a name="freeing-contexts"></a>释放上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


上下文在被删除后会被释放，并且对它的所有未完成引用都已释放。

此规则有一个例外：如果已创建上下文但尚未通过调用**FltSet***Xxx***上下文**进行设置，则无需删除它。 它在其引用计数达到零时被释放。 （请参阅[释放上下文](releasing-contexts.md)中的代码示例。）

当微筛选器驱动程序注册其上下文类型时，每个上下文定义可以选择性地包含要在释放上下文之前调用的上下文清理回调例程。 有关详细信息，请参阅[**PFLT\_CONTEXT\_清理\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)。

 

 




