---
title: Bug 检查 0x1D1 TELEMETRY_ASSERTS_LIVEDUMP
description: TELEMETRY_ASSERTS_LIVEDUMP bug 检查具有 0x000001D1 值。
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
ms.openlocfilehash: 0408dc7e51b0517255f4024d42249bf3e92c76ea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361981"
---
# <a name="bug-check-bug-check-0x1d1-telemetryassertslivedump"></a>Bug 检查 Bug 检查 0x1D1:遥测\_ASSERT 语句\_LIVEDUMP

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


TELEMETRY_ASSERTS_LIVEDUMP bug 检查具有 0x000001D1 值。 

遥测断言验证失败。

此代码可以永远不会用于实际的执行错误检查;它用于标识包括设备遥测数据的实时转储。

若要解决此问题，请检查调用堆栈以查看 MICROSOFT_TELEMETRY_ASSERT(expression) 中的表达式无效的原因。

## <a name="telemetryassertslivedump-parameters"></a>遥测\_assert 语句\_LIVEDUMP 参数

参数 | 描述 
|---------|--------------|
1 | Rva
2 | ModuleName
3 | TimeStamp
4 | SizeOfImage

 

 




