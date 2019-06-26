---
title: WDFVERIFY 宏
description: WDFVERIFY 宏测试的逻辑表达式和表达式的计算结果为 FALSE，如果强行进入内核调试器。
ms.assetid: 9dc19299-7eda-42fb-811e-ba8dc5c1cdb5
keywords:
- WDFVERIFY 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eec94b8472a09f64dba592a46cc7768a72149cbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354432"
---
# <a name="wdfverify-macro"></a>WDFVERIFY 宏


\[仅适用于 KMDF\]

**WDFVERIFY**宏测试的逻辑表达式和表达式的计算结果**FALSE**，进入内核调试器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WDFVERIFY(
    exp
);
```

<a name="parameters"></a>Parameters
----------

*exp*   
WDFVERIFY 测试逻辑表达式。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

代码**WDFVERIFY**生成您在发布配置或调试配置中的驱动程序时，宏包含驱动程序的二进制文件中。 如果您的驱动程序的二进制包括**WDFVERIFY**代码，代码将运行时检查内部版本号或免费版本的 Microsoft Windows 操作系统运行您的驱动程序。

**WDFVERIFY**代码进入内核调试器仅当**VerifyOn**在注册表中设置值。 有关可用于调试您的驱动程序的注册表项的详细信息，请参阅[Debugging Framework-Based 驱动程序的注册表项](https://docs.microsoft.com/windows-hardware/drivers/wdf/registry-values-for-debugging-kmdf-drivers)。

有关调试您的驱动程序的详细信息，请参阅[调试 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)。

<a name="examples"></a>示例
--------

如果尝试重新使用 request 对象失败，下面的代码示例将进入调试器。

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdfassert.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**VERIFY_IS_IRQL_PASSIVE_LEVEL**](verify-is-irql-passive-level.md)

 

 






