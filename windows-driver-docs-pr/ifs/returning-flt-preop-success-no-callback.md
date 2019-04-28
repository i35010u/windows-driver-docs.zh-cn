---
title: 返回 FLT_PREOP_SUCCESS_NO_CALLBACK
description: 返回 FLT_PREOP_SUCCESS_NO_CALLBACK
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed11d5ace93beb67fb08c70005538ce306367ebd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344569"
---
# <a name="returning-fltpreopsuccessnocallback"></a>返回 FLT\_PREOP\_成功\_否\_回调


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


如果微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)返回 FLT\_PREOP\_成功\_否\_回调，筛选器管理器不调用微筛选器驱动程序[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)，如果存在，在 I/O 完成。

如果微筛选器驱动程序的 preoperation 回调例程将返回 FLT\_PREOP\_成功\_否\_回调，它必须返回**NULL**中其*CompletionContext*输出参数。

FLT\_PREOP\_成功\_否\_回调状态值可以为所有类型的 I/O 操作返回。

 

 




