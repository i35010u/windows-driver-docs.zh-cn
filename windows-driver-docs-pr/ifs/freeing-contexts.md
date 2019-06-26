---
title: 释放上下文
description: 释放上下文
ms.assetid: e2b87662-c1bd-45a7-82a3-29817f7692fc
keywords:
- 上下文 WDK 文件系统微筛选器，释放
- 释放上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9100a9bf404c94bc6ec92ca74bdf7cf46a2b78c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384570"
---
# <a name="freeing-contexts"></a>释放上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


将其删除并已发布到其所有未完成的引用后，将释放上下文。

此规则的例外： 如果上下文已创建但尚未设置通过调用**FltSet***Xxx***上下文**，它不需要进行删除。 当其引用计数达到零时释放它。 (请参阅中的代码示例[释放上下文](releasing-contexts.md)。)

当微筛选器驱动程序注册其上下文类型时，每个上下文定义可以选择性地包含之前释放上下文调用的上下文清理回调例程。 有关详细信息，请参阅[ **PFLT\_上下文\_清理\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)。

 

 




