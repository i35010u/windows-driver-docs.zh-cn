---
title: WIA\_DPS\_扫描\_可用\_项
description: WIA\_DPS\_扫描\_可用\_项属性提供程序控制下执行应用程序推送扫描操作的输入源的名称。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 747cd5bb-4746-4086-8a87-08a6728125bc
keywords:
- WIA_DPS_SCAN_AVAILABLE_ITEM 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_SCAN_AVAILABLE_ITEM
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 200bb4172435ae06fe6bc04265e3b015078d392f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377933"
---
# <a name="wiadpsscanavailableitem"></a>WIA\_DPS\_扫描\_可用\_项


WIA\_DPS\_扫描\_可用\_项属性提供程序控制下执行应用程序推送扫描操作的输入源的名称。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

在 Windows 7 及更高版本，WIA\_DPS\_扫描\_可用\_项是 WIA 扫描程序设备 WIA 项树的根的项目的可选属性。 应用程序可以查询此属性来确定输入的源 （平板、 自动文档送纸器或电影扫描适配器） 进行扫描或将数据从传输的存储位置。

某些 WIA 扫描程序设备可使用户可以从设备的前面板中选择一个扫描作业的输入的源或隐式选择的输入的源，例如，通过将文档插入到在设备上送纸器。 当用户在设备上按开始扫描按钮时，该应用程序必须确定哪个输入用户选择，以便它可以启动此源的扫描操作的源。

扫描事件通知应用程序，用户已开始扫描速度，但该事件不会提供 WIA 项表示的输入的源的名称。 应用程序的事件处理程序可以查询根项 WIA\_DPS\_扫描\_可用\_项属性来获取输入的源项的名称。

在 WIA 树的根项目具有一个或多个子项 （平板项、 送纸器项目和电影胶片项），表示设备上的输入的源。 其中每个项目可能是表示部件或区域的输入源的子项目的父级。 是根项的子级，该值表示作为一个整体平板平板项可以有子级 （这也是平板项），用于表示单独的平板图面区域。 是根项的子级，该值表示自动文档送纸器送纸器项可以有子级，用于表示的前端和后端边进纸器通过在文档页扫描程序。 是根项的子级，该值表示作为一个整体的电影胶片扫描适配器电影项可以有子级 （这也是电影胶片项），用于表示单个电影帧。 具体取决于扫描操作请求的用户，WIA\_DPS\_扫描\_可用\_平板、 送纸器或电影是根的子级的项的项属性可以名或它可以进行命名的其中一种子项。 有关这些项目的详细信息，请参阅[WIA 项类别](https://msdn.microsoft.com/library/windows/hardware/ff552678)。

扫描事件发生时，该驱动程序将立即设置 WIA\_DPS\_扫描\_可用\_项属性值为 WIA 项名称 (完全由报告[ **WIA\_IPA\_项\_名称**](wia-ipa-item-name.md)项属性)，它标识从其扫描作业不可用，如果知道此信息的输入的源。 否则，如果输入的源未知，则该驱动程序设置的属性值为空字符串。 当应用程序使用扫描事件时中的扫描事件更改的状态终止状态为非终止，并驱动程序将重置 WIA\_DPS\_扫描\_可用\_项属性值为空字符串。

有关此属性的详细信息，请参阅[扫描事件标识输入源](https://msdn.microsoft.com/library/windows/hardware/ff542704)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_ITEM\_NAME**](wia-ipa-item-name.md)

 

 






