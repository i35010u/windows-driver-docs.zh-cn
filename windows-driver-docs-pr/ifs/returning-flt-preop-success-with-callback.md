---
title: 返回 FLT_PREOP_SUCCESS_WITH_CALLBACK
description: 返回 FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.assetid: 6247b952-3189-4792-a15b-c3a4b3dc80ae
keywords:
- FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc40035213be28d241e590c6b96f6dc065c69d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567978"
---
# <a name="returning-fltpreopsuccesswithcallback"></a>返回 FLT\_PREOP\_成功\_WITH\_回调


## <span id="ddk_returning_flt_preop_success_with_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_WITH_CALLBACK_IF"></span>


如果微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)返回 FLT\_PREOP\_成功\_WITH\_回调，筛选器管理器调用在微筛选器驱动程序[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)期间 I/O 完成。

**请注意**  如果 preoperation 微筛选器驱动程序的回调例程将返回 FLT\_PREOP\_成功\_WITH\_回调，但微筛选器驱动程序未注册该操作的 postoperation 回调例程，系统断言已检验版本上。

 

如果微筛选器驱动程序的 preoperation 回调例程将返回 FLT\_PREOP\_成功\_WITH\_回调，它可以返回非 NULL 值在其*CompletionContext*输出参数。 此参数是传递给相应的 postoperation 回调例程的可选上下文指针。 Postoperation 回调例程接收此指针在其*CompletionContext*输入的参数。

FLT\_PREOP\_成功\_WITH\_回调状态值可以为所有类型的 I/O 操作返回。

 

 




