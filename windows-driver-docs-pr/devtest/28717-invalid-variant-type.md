---
title: C28717
description: 警告 C28717 无效变体类型。
ms.assetid: e1373005-a1ff-4722-98f9-00c7e4f89370
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28717
ms.openlocfilehash: 7b8607446b9165fab9fbfc0ac6f2ad530b88c4cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371589"
---
# <a name="c28717"></a>C28717


警告 C28717:VARIANT 类型无效

**Vt**字段**变体结构**可能需要仅限特定值。 向它分配任何其他值是错误的。

**Vt**字段**变体**或**VARIANTARG**结构仅可以采用以下值 (可能是或运算的**VT\_BYREF**和/或**VT\_数组**):**VT\_空**， **VT\_NULL**， **VT\_I2**， **VT\_I4**， **VT\_R4**， **VT\_R8**， **VT\_CY**， **VT\_日期**， **VT\_BSTR**， **VT\_调度**， **VT\_错误**， **VT\_BOOL**， **VT\_VARIANT**， **VT\_十进制**， **VT\_记录、 VT\_未知**， **VT\_I1**， **VT\_UI1**， **VT\_UI2**， **VT\_UI4**， **VT\_INT**， **VT\_UINT** (**VT\_空**并**VT\_NULL**不能结合**VT\_数组**)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

PREfast 报告的警告的下面的示例。

```
VARIANT var;
var.vt = VT_SAFEARRAY | VT_INT;
```

下面的示例可避免此错误。

```
VARIANT var;
var.vt = VT_ARRAY | VT_INT;
```

 

 





