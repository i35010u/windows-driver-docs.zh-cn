---
title: VERIFY_IS_IRQL_PASSIVE_LEVEL 宏
description: VERIFY_IS_IRQL_PASSIVE_LEVEL 宏进入内核调试器，如果该驱动程序不在 IRQL passive_level 调用执行。
ms.assetid: 7f1e25af-df66-46a2-8d27-7924677e4d5d
keywords:
- VERIFY_IS_IRQL_PASSIVE_LEVEL 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfd95af57956eef7cef81fe1a112aaaaf1af2543
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546348"
---
# <a name="verifyisirqlpassivelevel-macro"></a>VERIFY_IS_IRQL_PASSIVE_LEVEL 宏


[仅适用于 KMDF]

**VERIFY_IS_IRQL_PASSIVE_LEVEL**宏进入内核调试器如果驱动程序不执行在 IRQL = passive_level 调用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID VERIFY_IS_IRQL_PASSIVE_LEVEL(void);
```

<a name="parameters"></a>参数
----------

此宏没有任何参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

代码**VERIFY_IS_IRQL_PASSIVE_LEVEL**生成您在发布配置或调试配置中的驱动程序时，宏包含驱动程序的二进制文件中。 如果您的驱动程序的二进制包括**VERIFY_IS_IRQL_PASSIVE_LEVEL**代码，代码将运行时检查内部版本号或免费版本的 Microsoft Windows 操作系统运行您的驱动程序。

**VERIFY_IS_IRQL_PASSIVE_LEVEL**代码中断到内核调试程序中，如果以下项之一为 true:

-   **DbgBreakOnError**在注册表中设置为非零值。
-   **VerifierOn**设置为非零值和**DbgBreakOnError**未设置。
-   启用驱动程序验证程序，该驱动程序生成框架版本 1.9 或更高版本，以及两者都**VerifierOn**也不**DbgBreakOnError**设置。

有关可用于调试您的驱动程序的注册表项的详细信息，请参阅[Debugging Framework-Based 驱动程序的注册表项](https://msdn.microsoft.com/library/windows/hardware/ff544573)。

有关调试您的驱动程序的详细信息，请参阅[调试 KMDF 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540790)。

<a name="examples"></a>示例
--------

下面的代码示例进入内核调试器如果驱动程序不执行在 IRQL = passive_level 调用。

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdfassert.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WDFVERIFY**](wdfverify.md)
