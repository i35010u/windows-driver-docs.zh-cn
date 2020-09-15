---
title: WDFVERIFY 宏
description: WDFVERIFY 宏可测试逻辑表达式，如果表达式的计算结果为 FALSE，则会中断内核调试器。
ms.assetid: 9dc19299-7eda-42fb-811e-ba8dc5c1cdb5
keywords:
- WDFVERIFY 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8443338eb55b81b5487c8661fc41d94e795bc7f
ms.sourcegitcommit: a5f76805387760730faed5674d87201ec85b7dd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90112108"
---
# <a name="wdfverify-macro"></a>WDFVERIFY 宏


\[仅适用于 KMDF\]

**WDFVERIFY**宏可测试逻辑表达式，如果表达式的计算结果为**FALSE**，则会中断内核调试器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WDFVERIFY(
    exp
);
```

<a name="parameters"></a>参数
----------

*.exp*   
WDFVERIFY 测试的逻辑表达式。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

当你在发布配置或调试配置中构建驱动程序时， **WDFVERIFY** 宏的代码将包含在驱动程序的二进制文件中。

仅当在注册表中设置了**VerifyOn**值时， **WDFVERIFY**代码才会进入内核调试器。 有关可用于调试驱动程序的注册表项的详细信息，请参阅 [用于调试基于框架的驱动程序的注册表项](./registry-values-for-debugging-kmdf-drivers.md)。

有关调试驱动程序的详细信息，请参阅 [调试 KMDF 驱动程序](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。

<a name="examples"></a>示例
--------

如果尝试重用请求对象失败，下面的代码示例将中断调试器。

```cpp
status = WdfRequestReuse(Request, &params);
WDFVERIFY(NT_SUCCESS(status));
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

## <a name="see-also"></a>另请参阅


[**VERIFY_IS_IRQL_PASSIVE_LEVEL**](verify-is-irql-passive-level.md)

 

