---
title: AddEuro
description: AddEuro
ms.assetid: 1d27fbb0-787f-4fb2-8a1c-3c68598d6d41
keywords:
- 微型驱动程序 WDK Pscript，AddEuro 功能
- AddEuro 功能 WDK 打印
- 欧元符号 WDK 打印
- 欧盟符号 WDK 打印
- ADHasEuro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b6f9b92332844915598b403820d54363f3832e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543271"
---
# <a name="addeuro"></a>AddEuro





欧元符号，如下图中所示是基本的货币单位的欧盟国家/地区中使用的货币符号。

![示意图，欧元符号](images/euro.png)

AddEuro 功能将此符号添加到打印机的设备字体。 启用 AddEuro 后，在显示设备会显示欧元符号将还打印在纸张上，文档发送到打印机时。 如果此功能不可用或已禁用，将选择非别名设备字体的用户将能够在屏幕上，请参阅欧元符号，但将在纸上看到一个大型循环点。 启用此功能，用户可以打印欧元符号，指示为打印机的设备字体中可用。

AddEuro 使用私有*PPD*关键字\* **ADHasEuro**，允许打印机制造商设置最佳的默认值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字和值</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>ADHasEuro</strong>:True</p></td>
<td><p>打印机已不需要下载一个内置欧元符号。 利用此值，默认情况下禁用 AddEuro。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ADHasEuro</strong>:False</p></td>
<td><p>打印机不具有内置的欧元符号;如果为调用应用程序，则应下载此符号。 利用此值，默认情况下，无论何种 PostScript 版本启用 AddEuro。</p></td>
</tr>
</tbody>
</table>

 

如果\* **ADHasEuro**关键字未出现，则前 3011，与 PostScript 版本的打印机的默认情况下，启用和禁用默认情况下，对于版本 3011 或之后 AddEuro 功能。

 

 




