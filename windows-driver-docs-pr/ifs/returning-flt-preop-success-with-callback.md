---
title: 返回 FLT_PREOP_SUCCESS_WITH_CALLBACK
description: 返回 FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.assetid: 6247b952-3189-4792-a15b-c3a4b3dc80ae
keywords:
- FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bff93862bf17d9472c5ea2e6ea5eaaf7654f8c27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840995"
---
# <a name="returning-flt_preop_success_with_callback"></a>\_回拨返回 FLT\_PREOP\_SUCCESS\_


## <span id="ddk_returning_flt_preop_success_with_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_WITH_CALLBACK_IF"></span>


如果微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)使用\_回调返回 FLT\_PREOP\_SUCCESS\_，则筛选器管理器将在 i/o 完成期间调用微筛选器驱动程序的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)。

**请注意**   如果微筛选器驱动程序的 preoperation 回调例程返回 FLT\_PREOP\_成功\_与\_回调，但微筛选器驱动程序未为操作注册 postoperation 回调例程，则系统会在已检查的内部版本中断言。

 

如果微筛选器驱动程序的 preoperation 回调例程使用\_回调返回 FLT\_PREOP\_SUCCESS\_，则它可以在其*CompletionContext* output 参数中返回非 NULL 值。 此参数是一个可选的上下文指针，它传递到相应的 postoperation 回调例程。 Postoperation 回调例程在其*CompletionContext*输入参数中接收此指针。

对于所有类型的 i/o 操作，都可以返回 FLT\_PREOP\_SUCCESS\_和\_回叫状态值。

 

 




