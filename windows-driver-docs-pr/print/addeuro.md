---
title: AddEuro
description: AddEuro
keywords:
- 微型驱动程序 WDK Pscript，AddEuro 功能
- AddEuro 功能 WDK 打印
- 欧元符号 WDK 打印
- 欧盟符号 WDK 打印
- ADHasEuro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1eecd489712c7b1bd68e78e8b1ef52b767d3b31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794239"
---
# <a name="addeuro"></a>AddEuro





欧元符号（如下图所示）是欧盟的国家/地区中使用的基本货币单位的货币符号。

![欧元符号图](images/euro.png)

AddEuro 功能将此符号添加到打印机的设备字体。 启用 AddEuro 时，在将文档发送到打印机时，显示设备上显示的欧元符号也将打印在纸张上。 如果此功能不可用或已禁用，则选择非别名设备字体的用户将可以在屏幕上看到 Euro 符号，但会在纸张上看到大圆点。 启用此功能后，用户可以打印欧元符号，无论其在打印机的设备字体中是否可用。

AddEuro 使用私有 *PPD* 关键字 \* **ADHasEuro**，以允许打印机制造商设置最佳默认值。

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
<td><p><em><strong>ADHasEuro</strong>： True</p></td>
<td><p>打印机已经具有不需要下载的内置欧元符号。 使用此值，默认情况下，AddEuro 处于禁用状态。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ADHasEuro </strong> ： False</p></td>
<td><p>打印机没有内置的欧元符号;如果是由应用程序调用的，则应下载此符号。 如果使用此值，则默认情况下将启用 AddEuro，而不考虑 PostScript 版本。</p></td>
</tr>
</tbody>
</table>

 

如果 \* 未显示 *_ADHasEuro_* 关键字，则默认情况下，对于使用3011之前的 PostScript 版本的打印机启用 AddEuro 功能，默认情况下，对于版本3011或之后禁用该功能。

 

 




