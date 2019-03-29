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
ms.openlocfilehash: 614a3eb586765eaa3a9a7bac1db884de6a53cc12
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743510"
---
# <a name="bug-check-0x17e-microcoderevisionmismatch"></a>Bug 检查 0x17E:微码\_修订\_不匹配

微代码，\_修订\_不匹配错误检查的值为 0x0000017E。 它指示多处理器配置中的一个或多个处理器都有不一致的微代码加载。  

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。
 

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

