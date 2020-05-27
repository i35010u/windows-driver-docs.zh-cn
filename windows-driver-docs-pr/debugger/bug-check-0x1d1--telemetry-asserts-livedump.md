---
title: Bug 检查 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
description: TELEMETRY_ASSERTS_LIVEDUMP bug 检查的值为0x000001D1。
keywords:
- Bug 检查 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
- TELEMETRY_ASSERTS_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- TELEMETRY_ASSERTS_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66fdc0b2c6d5792b4ecd9acb40e3e1727dcd844b
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851264"
---
# <a name="bug-check-0x1d1-telemetry_asserts_livedump"></a>Bug 检查0x1D1：遥测 \_ 断言 \_ LIVEDUMP

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


TELEMETRY_ASSERTS_LIVEDUMP bug 检查的值为0x000001D1。 

遥测断言验证失败。

此代码永远不能用于实际错误检查;它用于标识包含设备遥测的实时转储。

若要解决此问题，请检查调用堆栈，以了解 MICROSOFT_TELEMETRY_ASSERT （expression）中的表达式无效的原因。

## <a name="telemetry_asserts_livedump-parameters"></a>遥测 \_ 断言 \_ LIVEDUMP 参数

参数 | 说明 
|---------|--------------|
1 | Rva
2 | ModuleName
3 | 时间戳
4 | SizeOfImage

 

 




