---
title: Bug 检查 0x93 INVALID_KERNEL_HANDLE
description: INVALID_KERNEL_HANDLE bug 检查的值为0x00000093。 此 bug 检查表明传递到 NtClose 的句柄无效或受保护。
keywords:
- Bug 检查 0x93 INVALID_KERNEL_HANDLE
- INVALID_KERNEL_HANDLE
ms.date: 10/10/2019
topic_type:
- apiref
api_name:
- INVALID_KERNEL_HANDLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2380cb20a3bf1bc4ed088fbdcbcd085a83e6e51f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813309"
---
# <a name="bug-check-0x93-invalid_kernel_handle"></a>Bug 检查0x93： \_ 内核 \_ 句柄无效

无效 \_ 内核 \_ 句柄 bug 检查的值为0x00000093。 此 bug 检查表明传递到 **NtClose** 的句柄无效或受保护。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="invalid_kernel_handle-parameters"></a>\_内核 \_ 句柄参数无效

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|调用 NtClose 的句柄 |0                |0   | 0  | 已关闭受保护的句柄。|
|调用 NtClose 的句柄 |1                |0   | 0  | 关闭或引用了无效的句柄。|
|引用的句柄          |句柄表 |0   | 1  | 引用无效内核句柄时发生错误，已启用错误的句柄检测。|

## <a name="cause"></a>原因

INVALID_KERNEL_HANDLE bug 检查指示某些内核代码 (例如，服务器、重定向程序或另一驱动程序) 尝试关闭无效句柄或受保护的句柄。

如果参数4的值为1，则表示发生了引用无效内核句柄的错误，并且启用了错误的句柄检测。

如果内核代码尝试关闭或引用的句柄不是有效的句柄，则会出现此消息。 除非启用了错误的句柄检测，否则仅传递到 NtClose 的无效或受保护的句柄会导致此错误检查。
