---
title: Bug 检查 0x170 CRYPTO_LIBRARY_INTERNAL_ERROR
description: CRYPTO_LIBRARY_INTERNAL_ERROR bug 检查的值为0x00000170。 它表示加密库中出现内部错误。
keywords:
- Bug 检查 0x170 CRYPTO_LIBRARY_INTERNAL_ERROR
- CRYPTO_LIBRARY_INTERNAL_ERROR
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- CRYPTO_LIBRARY_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b129a1ab729933417235017f8bd671f86cf924a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208734"
---
# <a name="bug-check-0x170-crypto_library_internal_error"></a>Bug 检查0x170：加密 \_ 库 \_ 内部 \_ 错误 

"加密 \_ 库 \_ 内部错误错误检查" 的值为 " \_ 0x00000170"。 它表示加密库中出现内部错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。



 ## <a name="crypto_library_internal_error--parameters"></a>加密 \_ 库 \_ 内部 \_ 错误参数

|参数|说明|
|--- |--- |
|1| 失败的 ID。|
|2| 保留。|
|3| 保留。 |
|4| 保留。 |


## <a name="cause"></a>原因
-----

此错误检查指示加密库出现异常，此异常永远不会发生，并且库不会向调用方发送错误的安全方法。  这可能是活动攻击的症状。


## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[加密 API：下一代](/windows/desktop/SecCNG/cng-portal)