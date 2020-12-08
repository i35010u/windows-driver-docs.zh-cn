---
title: C28133
description: 警告 C28133 IoInitializeTimer 最适用于 AddDevice。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28133
ms.openlocfilehash: 4cac7bfe0ee68eb48a5aa29eafed65b139caeefe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816931"
---
# <a name="c28133"></a>C28133


警告 C28133： IoInitializeTimer 最适用于 AddDevice

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>对于每个设备对象，IoInitializeTimer 只能调用一次。 从 AddDevice 例程调用它有助于确保不会意外调用多次。</p></td>
</tr>
</tbody>
</table>

 

驱动程序正在调用 [**IoInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer) ，而不是其 **AddDevice** 例程。 代码分析工具使用此机会建议一种最佳做法建议，这些建议可防止错误并使驱动程序代码更可靠。

 

