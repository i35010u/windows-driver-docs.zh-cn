---
title: 执行完成某个 I/O 操作的处理
description: 执行完成某个 I/O 操作的处理
ms.assetid: 7e65c21c-d38f-4804-8c07-6cd89f6a6dd6
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，完成处理
- 完成 I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0950c3ad81ed4f5b7ddd4e3e65e291540c68dd85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543635"
---
# <a name="performing-completion-processing-for-an-io-operation"></a>执行完成某个 I/O 操作的处理


## <span id="ddk_performing_completion_processing_for_an_io_operation_if"></span><span id="DDK_PERFORMING_COMPLETION_PROCESSING_FOR_AN_IO_OPERATION_IF"></span>


微筛选器驱动程序[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)通过基础文件系统、 传统的筛选器，或另一个微筛选器驱动程序，它是在完成某个 I/O 操作时调用在微筛选器驱动程序实例堆栈中的较低海拔高度。

此外，当正在销毁微筛选器驱动程序实例，筛选器管理器"清空"实例已收到为其任何 I/O 操作[ **preoperation 回调**](https://msdn.microsoft.com/library/windows/hardware/ff551109)和正在等待[**postoperation 回调**](https://msdn.microsoft.com/library/windows/hardware/ff551107)。 在此情况下，筛选器管理器调用微筛选器驱动程序的 postoperation 回调例程，即使在 I/O 操作尚未完成，并设置 FLTFL\_POST\_操作\_中的排出标志*标志*输入的参数。

当 FLTFL\_POST\_操作\_排出标志设置，则微筛选器驱动程序将不能执行正常完成处理。 相反，它应执行仅需清理，如释放内存微筛选器驱动程序分配给*CompletionContext*参数中其 preoperation 回调例程，并返回 FLT\_POSTOP\_完成\_处理。

本部分包括以下主题：

[确保安全的 IRQL 在执行完成处理](ensuring-that-completion-processing-is-performed-at-safe-irql.md)

 

 




