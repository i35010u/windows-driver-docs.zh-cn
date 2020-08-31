---
title: 返回 FLT_PREOP_SUCCESS_WITH_CALLBACK
description: 返回 FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.assetid: 6247b952-3189-4792-a15b-c3a4b3dc80ae
keywords:
- FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9c5ed62d7c44474dd41a35f79343fc701fdf66
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066868"
---
# <a name="returning-flt_preop_success_with_callback"></a>\_ \_ \_ 通过回调返回 FLT PREOP \_ SUCCESS


## <span id="ddk_returning_flt_preop_success_with_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_WITH_CALLBACK_IF"></span>


如果微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 返回 FLT \_ PREOP \_ SUCCESS \_ WITH \_ callback，则筛选器管理器将在 i/o 完成期间调用微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 。

**注意**   如果微筛选器驱动程序的 preoperation 回调例程返回 FLT \_ PREOP \_ SUCCESS \_ WITH \_ callback，但微筛选器驱动程序未为操作注册 postoperation 回调例程，则系统会在已检查的内部版本中断言。

 

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT \_ PREOP \_ SUCCESS \_ WITH \_ callback，它可以在其 *CompletionContext* output 参数中返回非 NULL 值。 此参数是一个可选的上下文指针，它传递到相应的 postoperation 回调例程。 Postoperation 回调例程在其 *CompletionContext* 输入参数中接收此指针。

\_ \_ \_ \_ 对于所有类型的 i/o 操作，都可以返回 FLT PREOP SUCCESS WITH 回叫状态值。

 

