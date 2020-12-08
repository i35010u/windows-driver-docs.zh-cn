---
title: WIA \_ DPS \_ 扫描 \_ 可用 \_ 项
description: WIA \_ DPS \_ SCAN \_ 可用 \_ 项属性提供应用程序在程序控制下执行的推送扫描操作的输入源的名称。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPS_SCAN_AVAILABLE_ITEM 图像设备
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
ms.openlocfilehash: 47f1ff1b1848ec7a6ecc544956e8bdc0531aa762
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831735"
---
# <a name="wia_dps_scan_available_item"></a>WIA \_ DPS \_ 扫描 \_ 可用 \_ 项


WIA \_ DPS \_ SCAN \_ 可用 \_ 项属性提供应用程序在程序控制下执行的推送扫描操作的输入源的名称。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

在 Windows 7 和更高版本中，WIA \_ DPS \_ SCAN \_ 可用 \_ 项是 WIA 扫描器设备的 wia 项树中的根项的可选属性。 应用程序可以查询此属性，以确定输入源 (平板、自动文档送纸器或胶片扫描适配器) 从中进行扫描，或从其传输数据的存储位置。

某些 WIA 扫描器设备使用户能够从设备的前面板中为扫描作业选择输入源，或者通过将文档插入设备上的进纸器来隐式选择输入源。 当用户按下设备上的 "开始扫描" 按钮时，应用程序必须确定用户选择了哪个输入源，以便它可以在此源上启动扫描操作。

Scan 事件会通知应用程序用户已启动扫描，但该事件不提供表示输入源的 WIA 项的名称。 应用程序的事件处理程序可以查询根项的 WIA \_ DPS \_ SCAN \_ 可用 \_ 项属性以获取输入源项的名称。

WIA 树中的根项具有一个或多个子项 (平板项、进纸器项和胶卷项) ，表示设备上的输入源。 其中每个项都可能是表示输入源的部件或区域的父项。 作为根项的子项并且表示整个外围的平板项可以具有子 (，它们也是表示平板表面的各个区域) 平台项。 作为根项的子项并且表示自动文档送纸器的 "送纸器" 项可以具有代表文档页面正面和背面的扫描仪的子送纸器。 作为根项的子项并且表示作为整体的胶卷扫描适配器的一个胶卷项可以具有子级 (，它们也是表示各个胶片帧) 的电影项。 根据用户请求的扫描操作，WIA \_ DPS \_ SCAN \_ 可用 \_ 项属性可以命名作为根子项的平板、进纸器或胶卷项，也可以命名其中一个项的子项。 有关这些项的详细信息，请参阅 [WIA 项类别](./wia-item-categories.md)。

当发生扫描事件时，驱动程序会立即将 WIA \_ DPS \_ 扫描 \_ 可用 \_ 项属性值设置为 wia 项名称 (由项) 的 [**wia \_ IPA \_ 项 \_ 名称**](wia-ipa-item-name.md) 属性标识，该项用于标识扫描作业可用的输入源，如果此信息已知，则为。 否则，如果输入源未知，则驱动程序将属性值设置为空字符串。 当应用程序使用 scan 事件时，scan 事件的状态将从 "已发出到非终止" 更改，驱动程序会将 "WIA \_ DPS \_ 扫描 \_ 可用 \_ 项" 属性值重置为空字符串。

有关此属性的详细信息，请参阅 [标识扫描事件的输入源](./identifying-the-input-source-for-a-scan-event.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 项 \_ 名称**](wia-ipa-item-name.md)

 

