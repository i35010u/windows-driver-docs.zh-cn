---
title: Bug 检查 0x14C FATAL_ABNORMAL_RESET_ERROR
description: FATAL_ABNORMAL_RESET_ERROR bug 检查的值为0x0000014C。 这表明发生了不可恢复的系统错误或系统异常重置。
keywords:
- Bug 检查 0x14C FATAL_ABNORMAL_RESET_ERROR
- FATAL_ABNORMAL_RESET_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FATAL_ABNORMAL_RESET_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdc327cf86739e8dcfa761cbd8fce55012abd581
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790717"
---
# <a name="bug-check-0x14c-fatal_abnormal_reset_error"></a>Bug 检查0x14C：致命 \_ 异常 \_ 重置 \_ 错误


致命 \_ 异常 \_ 重置 \_ 错误 bug 检查的值为0x0000014C。 这表明发生了不可恢复的系统错误或系统异常重置。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="fatal_abnormal_reset_error-parameters"></a>致命 \_ 异常 \_ 重置 \_ 错误参数


无

<a name="cause"></a>原因
-----

系统遇到错误并重新启动。 可能导致此错误的问题包括：应用程序或辅助处理器中的硬件监视程序计时器，指示系统挂起、用户启动的键顺序，因为存在挂起、brownout 或在默认检测路径中出现故障。 缓存可能不会刷新，并且生成的完整内存转储可能不包含当前线程上下文。

标记 {E1D08891-D5A3-45F9-B811-AD711DFB2607} 的辅助数据包含其他 "黑盒" 数据。 使用 [**. enumtag (枚举辅助回叫数据)**](-enumtag--enumerate-secondary-callback-data-.md) 以查看数据。

 

 




