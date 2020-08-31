---
title: 返回 FLT_PREOP_SUCCESS_NO_CALLBACK
description: 返回 FLT_PREOP_SUCCESS_NO_CALLBACK
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48713c68d3eeb3ad58cf5b973c8322af374f50fb
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063238"
---
# <a name="returning-flt_preop_success_no_callback"></a>返回 FLT \_ PREOP \_ SUCCESS \_ NO \_ 回拨


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


如果微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 返回 FLT \_ PREOP \_ SUCCESS \_ NO \_ 回拨，则筛选器管理器不会在 i/o 完成期间调用微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)（如果存在）。

如果微筛选器驱动程序的 preoperation 回调例程返回 FLT \_ PREOP \_ SUCCESS \_ NO \_ 回拨，则它必须在其*CompletionContext* output 参数中返回**NULL** 。

\_ \_ \_ \_ 对于所有类型的 i/o 操作，都无法返回 FLT PREOP SUCCESS。

 

