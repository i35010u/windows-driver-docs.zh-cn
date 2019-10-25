---
title: 返回 FLT_PREOP_SUCCESS_NO_CALLBACK
description: 返回 FLT_PREOP_SUCCESS_NO_CALLBACK
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f178fb5676bad3424b757b98442ef086171dc492
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840998"
---
# <a name="returning-flt_preop_success_no_callback"></a>返回 FLT\_PREOP\_成功\_不\_回拨


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


如果微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)返回 FLT\_PREOP\_SUCCESS\_不\_回拨，则筛选器管理器不会调用微筛选器驱动程序的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)（如果存在）。在 i/o 完成期间。

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT\_PREOP\_SUCCESS\_不\_回拨，则必须在其*CompletionContext* output 参数中返回**NULL** 。

FLT\_PREOP\_成功\_不能为所有类型的 i/o 操作返回\_回叫状态值。

 

 




