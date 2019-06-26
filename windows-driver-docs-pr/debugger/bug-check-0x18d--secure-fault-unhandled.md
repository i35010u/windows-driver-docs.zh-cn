---
title: Bug 检查 0x18D SECURE_FAULT_UNHANDLED
description: SECURE_FAULT_UNHANDLED bug 检查具有 0x0000018D 值。 它指示无法处理由安全内核产生的安全错误。
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
ms.openlocfilehash: bd5f32c0abebe0f084c8a3cf9b90eb8eba968a6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367680"
---
# <a name="bug-check-0x18d-securefaultunhandled"></a>Bug 检查 0x18D：安全\_容错\_未处理

SECURE\_容错\_未经处理的错误检查的值为 0x0000018D。

无法处理此 bug 检查 indidates 安全错误由安全内核发起的。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


 ## <a name="securefaultunhandled-parameters"></a>安全\_容错\_未经处理的参数

| 参数 | 描述 |
|-----------|-------------|
| 1 | 安全错误代码的位掩码-下面的值。 |
| 2 | 安全错误 VA （仅适用于特定的安全错误类型）。 |
| 3 | 异常记录。 |
| 4 | 上下文记录。 |


**安全错误代码的位掩码**

```text
     0x1 : KSECURE_FAULT_SLAT_NX
         A no-execute fault occured due to SLAT page protections.
     0x2 : KSECURE_FALT_SLAT_READ
         A read fault occurred due to SLAT page protections.
     0x4 : KSECURE_FAULT_SLAT_WRITE
         A write fault occured due to SLAT page protections.
     0x8 : KSECURE_FAULT_DOUBLE_FAULT
         A secure fault occurred before the prior secure fault had been dismissed by the kernel.
```

## <a name="cause"></a>原因
-----

无法处理由安全内核产生的安全错误。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)
