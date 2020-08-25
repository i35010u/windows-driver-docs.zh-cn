---
title: Bug 检查 0x18D SECURE_FAULT_UNHANDLED
description: SECURE_FAULT_UNHANDLED bug 检查的值为0x0000018D。 它表示无法处理由安全内核产生的安全故障。
keywords:
- Bug 检查 0x18D SECURE_FAULT_UNHANDLED
- SECURE_FAULT_UNHANDLED
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- SECURE_FAULT_UNHANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1aaa1251a033c878f7950fd810d58aa2b35f25f2
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802777"
---
# <a name="bug-check-0x18d-secure_fault_unhandled"></a>Bug 检查0x18D： \_ \_ 未处理安全错误

安全 \_ 错误 \_ 未处理 bug 检查的值为0x0000018D。

此错误检查 indidates 无法处理由安全内核产生的安全故障。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅 [排查蓝屏错误](https://www.windows.com/stopcode)。


 ## <a name="secure_fault_unhandled-parameters"></a>安全 \_ 错误 \_ 未处理参数

| 参数 | 说明 |
|-----------|-------------|
| 1 | 安全错误代码位掩码-下面的值。 |
| 2 | 安全错误 VA (仅适用于某些) 的安全错误类型。 |
| 3 | 异常记录。 |
| 4 | 上下文记录。 |


**安全错误代码位掩码**

```text
     0x1 : KSECURE_FAULT_SLAT_NX
         A no-execute fault occurred due to SLAT page protections.
     0x2 : KSECURE_FALT_SLAT_READ
         A read fault occurred due to SLAT page protections.
     0x4 : KSECURE_FAULT_SLAT_WRITE
         A write fault occurred due to SLAT page protections.
     0x8 : KSECURE_FAULT_DOUBLE_FAULT
         A secure fault occurred before the prior secure fault had been dismissed by the kernel.
```

## <a name="cause"></a>原因
-----

无法处理安全内核产生的安全错误。


## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)
