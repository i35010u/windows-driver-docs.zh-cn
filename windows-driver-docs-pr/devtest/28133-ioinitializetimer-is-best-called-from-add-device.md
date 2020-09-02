---
title: C28133
description: 警告 C28133 IoInitializeTimer 最适用于 AddDevice。
ms.assetid: c832cf67-1fc2-491b-a9e3-d35c5d9f6b73
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28133
ms.openlocfilehash: 264fb468691f7a040299a1ac9ca82793f877f4d1
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382597"
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

 

