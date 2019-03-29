---
title: IPrintOemCommon COM 接口
description: IPrintOemCommon COM 接口
ms.assetid: 1d4b2f77-6682-4a4b-8d7f-34acd03523e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 498bb3ba233bc8ccaeda2b234a6ff90a5adb6222
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349892"
---
# <a name="iprintoemcommon-com-interface"></a>IPrintOemCommon COM 接口


`IPrintOemCommon` COM 接口，插件来指定或获取设备信息。 此接口提供用户界面和呈现插件之间通用的功能。

下表列出并描述所有方法的`IPrintOemCommon`接口定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IPrintOemCommon::DevMode</strong></p></td>
<td><p>对专用 DEVMODEW 成员执行操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>IPrintOemCommon::GetInfo</strong></p></td>
<td><p>返回一个即插即用项的标识信息。</p></td>
</tr>
</tbody>
</table>

 

有关如何为 UI 插件实现这些方法的信息，请参阅[IPrintOemUI COM 接口](iprintoemui-com-interface.md)。

 

 




