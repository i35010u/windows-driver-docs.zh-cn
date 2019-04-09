---
title: Bug 检查 0x17E MICROCODE_REVISION_MISMATCH
description: MICROCODE_REVISION_MISMATCH bug 检查具有 0x0000017E 值。 它指示多处理器配置中的一个或多个处理器都有不一致的微代码加载。
keywords:
- Bug 检查 0x17E MICROCODE_REVISION_MISMATCH
- MICROCODE_REVISION_MISMATCH
ms.date: 01/14/2019
topic_type:
- apiref
api_name:
- MICROCODE_REVISION_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 789f40140d04863132733f9f659b056747c7b177
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239546"
---
# <a name="bug-check-0x17e-microcoderevisionmismatch"></a>Bug 检查 0x17E:微码\_修订\_不匹配

微代码，\_修订\_不匹配错误检查的值为 0x0000017E。 它指示多处理器配置中的一个或多个处理器都有不一致的微代码加载。  

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="microcoderevisionmismatch-parameters"></a>微码\_修订\_不匹配参数

|参数|描述|
|-------- |---------- |
|1| 处理器的处理器的不匹配的 CPUID 签名值。 |
|2| 处理器预期微代码修订。 |
|3| 实际报告处理器的微代码修订。 |
|4| 不匹配的处理器的处理器索引。|


## <a name="cause"></a>原因
-----
在多处理器配置中的一个或多个处理器都有不一致的微代码加载。 此检测错误指示该错误系统固件已错误地应用于主机配置中的处理器的一个子集的微代码更新。 系统固件必须应用于一种统一的方式中的所有处理器的微代码更新。 

## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

