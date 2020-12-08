---
title: Bug 检查 0x175 PREVIOUS_FATAL_ABNORMAL_RESET_ERROR
description: PREVIOUS_FATAL_ABNORMAL_RESET_ERROR bug 检查的值为0x00000175。
keywords:
- Bug 检查 0x175 PREVIOUS_FATAL_ABNORMAL_RESET_ERROR
- PREVIOUS_FATAL_ABNORMAL_RESET_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PREVIOUS_FATAL_ABNORMAL_RESET_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 51a060b5f32edd5fe1b3bfd4c33b1fbbb8c3052f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830755"
---
# <a name="bug-check-0x175-previous_fatal_abnormal_reset_error"></a>Bug 检查0x175：上一个 \_ 严重的 \_ 异常 \_ 重置 \_ 错误


先前的 \_ 致命 \_ 异常 \_ 重置 \_ 错误检查的值为0x00000175。 这表明发生了不可恢复的系统错误或系统在 Windows phone 设备上的异常重置。 系统生成了一个实时转储，用于收集先前错误中的设备故障数据。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="previous_fatal_abnormal_reset_error-parameters"></a>以前的 \_ 致命 \_ 异常 \_ 重置 \_ 错误参数


| 参数 | 描述 |
|-----------|-------------|
| 1         | 保留    |
| 2         | 预留    |
| 3         | 预留    |
| 4         | 预留    |

 

<a name="cause"></a>原因
-----

Windows Phone 设备上的系统遇到意外错误，并已重新启动。 可能导致此错误的问题包括：应用程序或辅助处理器中的硬件监视程序计时器，指示系统挂起、用户启动的键序列（因为挂起）等。

 

 




