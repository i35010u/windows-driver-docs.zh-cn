---
title: VERIFY_IS_IRQL_PASSIVE_LEVEL 宏
description: 如果驱动程序未以 IRQL PASSIVE_LEVEL 执行，VERIFY_IS_IRQL_PASSIVE_LEVEL 宏将进入内核调试器。
keywords:
- VERIFY_IS_IRQL_PASSIVE_LEVEL 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84aec2d866d82e456ebd173a3c4bc3b01a6c16fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790137"
---
# <a name="verify_is_irql_passive_level-macro"></a>VERIFY_IS_IRQL_PASSIVE_LEVEL 宏


[仅适用于 KMDF]

如果驱动程序未以 IRQL = PASSIVE_LEVEL 执行，则 **VERIFY_IS_IRQL_PASSIVE_LEVEL** 宏将进入内核调试器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID VERIFY_IS_IRQL_PASSIVE_LEVEL(void);
```

<a name="parameters"></a>参数
----------

此宏没有参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

在发布配置或调试配置中构建驱动程序时，将在驱动程序的二进制文件中包含 **VERIFY_IS_IRQL_PASSIVE_LEVEL** 宏的代码。 

如果满足以下条件之一，则 **VERIFY_IS_IRQL_PASSIVE_LEVEL** 代码将进入内核调试器：

-   在注册表中， **DbgBreakOnError** 设置为非零值。
-   **VerifierOn** 设置为一个非零值，并且未设置 **DbgBreakOnError** 。
-   驱动程序验证程序已启用，驱动程序是用 framework 1.9 或更高版本生成的，并且不设置 **VerifierOn** 和 **DbgBreakOnError** 。

有关可用于调试驱动程序的注册表项的详细信息，请参阅 [用于调试 Framework-Based 驱动程序的注册表项](./registry-values-for-debugging-kmdf-drivers.md)。

有关调试驱动程序的详细信息，请参阅 [调试 KMDF 驱动程序](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。

<a name="examples"></a>示例
--------

如果驱动程序未在 IRQL = PASSIVE_LEVEL 上执行，则下面的代码示例将中断内核调试器。

```cpp
VERIFY_IS_IRQL_PASSIVE_LEVEL();
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdfassert (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDFVERIFY**](wdfverify.md)
