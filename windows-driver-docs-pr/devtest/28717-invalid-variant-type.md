---
title: C28717
description: 警告 C28717 变体类型无效。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28717
ms.openlocfilehash: 7699570b450d43de7a1fec4828fd605f1f44a313
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837325"
---
# <a name="c28717"></a>C28717


警告 C28717：无效的 VARIANT 类型

**变量结构** 的 **vt** 字段只能采用某些值。 向其分配其他任何值都是错误的。

**VARIANT** 或 **VARIANTARG** 结构的 **vt** 字段只能采用以下值 (可能由 **Vt \_ BYREF** 和/或 **vt \_ 数组** 运算) ： **vt \_ EMPTY 为空**， **vt \_ NULL**、 **vt \_ I2**、 **vt \_ I4**、 **vt \_ R4**、 **vt \_ R8**、 **vt \_ CY**、 **vt \_ DATE**、vt **\_ BSTR**、Vt **\_ 调度**、 **vt \_ 错误**、vt **\_ BOOL**、vt **\_ VARIANT**、vt **\_ DECIMAL**、 **vt RECORD、 \_ vt \_ UNKNOWN**、vt **\_ I1**、vt **\_ UI1**、 **vt \_ UI2**、vt **\_ UI4**、vt **\_ INT**、vt **\_ UINT** (**vt \_ EMPTY** 和 **vt \_ NULL** 不能与 **vt \_ ARRAY**) 组合。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

PREfast 报告以下示例的警告。

```
VARIANT var;
var.vt = VT_SAFEARRAY | VT_INT;
```

下面的示例可避免此错误。

```
VARIANT var;
var.vt = VT_ARRAY | VT_INT;
```

 

 





