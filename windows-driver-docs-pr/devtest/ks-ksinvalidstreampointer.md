---
title: 'KsInvalidStreamPointer 规则 (ks) '
description: 此规则验证 KS 微型端口驱动程序是否提供有效的 KS 流指针作为函数参数。
ms.date: 04/01/2020
keywords:
- 'KsInvalidStreamPointer 规则 (ks) '
topic_type:
- apiref
api_name:
- KsInvalidStreamPointer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a87dd870ff3de0d4301d28e9ff1037c8abf0ba90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811175"
---
# <a name="ksinvalidstreampointer-rule-ks"></a>KsInvalidStreamPointer 规则 (ks) 

**KsInvalidStreamPointer** 规则验证 ks 微型端口驱动程序是否提供有效的 Ks 流指针作为函数参数。 典型冲突是由不正确的指针处理或内存使用不当引起的指针损坏引起的。

有效的流指针是前导或尾随边缘流指针，或者是通过 [KsStreamPointerClone](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)克隆的流指针。 有关详细信息，请参阅 [前导边缘和尾随边缘流指针](/windows-hardware/drivers/stream/leading-and-trailing-edge-stream-pointers)。

此规则还验证是否尚未使用 [KsStreamPointerDelete](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete) 来尝试删除非克隆的流指针。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x0008100C) 


<a name="example"></a>示例
-------

下面的代码与此规则冲突。

```cpp
PKKSSTREAM_POINTER StreamPointer = KsPinGetLeadingEdgeStreamPointer (Pin, KSSTREAM_POINTER_STATE_UNLOCKED);

//
// ERROR: KsStreamPointerDelete can only be called on clone stream pointers.
//

KsStreamPointerDelete (StreamPointer);
```

此代码也违反了该规则。 

```cpp
KsStreamPointerDelete (NULL);
```

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain ks</strong>。</p>
<p>例如：</p>
<p></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

**验证程序/domain ks** \[*选项* \]**/driver** *&lt; yourdriver &gt;*

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

KsStreamPointerDelete

KsStreamPointerAdvance

KsStreamPointerAdvanceOffsetsAndUnlock

KsStreamPointerCancelTimeout

KsStreamPointerGetIrp

KsStreamPointerGetMdl

KsStreamPointerGetNextClone

KsStreamPointerLock

KsStreamPointerScheduleTimeout

KsStreamPointerSetStatusCode

KsStreamPointerUnlock
