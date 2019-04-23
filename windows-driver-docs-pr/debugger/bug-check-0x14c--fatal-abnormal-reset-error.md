---
title: Bug 检查 0x14C FATAL_ABNORMAL_RESET_ERROR
description: FATAL_ABNORMAL_RESET_ERROR bug 检查具有 0x0000014C 值。 这表示出现不可恢复的系统错误或系统异常已重置。
ms.assetid: 46E624EE-CA84-443E-95C2-E128E8D03188
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
ms.openlocfilehash: 37ff89117ab3d2ecfbba74c1126fd4423a321478
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902593"
---
# <a name="bug-check-0x14c-fatalabnormalreseterror"></a>Bug 检查 0x14C：致命\_异常\_重置\_错误


严重\_异常\_重置\_错误 bug 检查的值为 0x0000014C。 这表示出现不可恢复的系统错误或系统异常已重置。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="fatalabnormalreseterror-parameters"></a>致命\_异常\_重置\_错误参数


无

<a name="cause"></a>原因
-----

系统中遇到意外的错误并重新启动。 可能会导致此错误的问题包括： 应用程序或辅助处理器由于挂起、 电力不足情况或默认错误检查路径中的失败表示系统挂起，用户启动的键序列中的硬件监视计时器。 可能不会刷新缓存，并生成完整的内存转储不能包含当前线程上下文。

辅助标记 {E1D08891-D5A3-45F9-B811-AD711DFB2607} 的数据包含其他"黑盒"的数据。 使用[ **.enumtag （枚举辅助回调数据）** ](-enumtag--enumerate-secondary-callback-data-.md)若要查看的数据。

 

 




