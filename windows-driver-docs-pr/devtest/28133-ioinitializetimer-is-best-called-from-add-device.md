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
ms.openlocfilehash: 6b07ca8a0cb47481e0b5673938d8a292b604cbd5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839596"
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
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>对于每个设备对象，IoInitializeTimer 只能调用一次。 从 AddDevice 例程调用它有助于确保不会意外调用多次。</p></td>
</tr>
</tbody>
</table>

 

驱动程序正在调用[**IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer) ，而不是其**AddDevice**例程。 代码分析工具使用此机会建议一种最佳做法建议，这些建议可防止错误并使驱动程序代码更可靠。

 

 





