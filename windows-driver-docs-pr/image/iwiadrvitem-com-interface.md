---
title: IWiaDrvItem COM 接口
description: IWiaDrvItem COM 接口
ms.assetid: 1be2265b-7ae8-4935-9559-588b885526d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd3ae78f0c84269c5743fba8443d4e6811f22746
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381815"
---
# <a name="iwiadrvitem-com-interface"></a>IWiaDrvItem COM 接口





[IWiaDrvItem 接口](https://msdn.microsoft.com/library/windows/hardware/ff543896)提供 WIA 微型驱动程序使用来管理的树的方法**IWiaDrvItem**项。 这些方法允许 WIA 微型驱动程序来处理**IWiaDrvItem**对象。 **IWiaDrvItem**接口提供以下方法。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543856" data-raw-source="[&lt;strong&gt;IWiaDrvItem::AddItemToFolder&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543856)"><strong>IWiaDrvItem::AddItemToFolder</strong></a></p></td>
<td><p>将添加<strong>IWiaDrvItem</strong>对象与文件夹。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543863" data-raw-source="[&lt;strong&gt;IWiaDrvItem::DumpItemData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543863)"><strong>IWiaDrvItem::DumpItemData</strong></a></p></td>
<td><p>转储专用驱动程序项数据。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543867" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindChildItemByName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543867)"><strong>IWiaDrvItem::FindChildItemByName</strong></a></p></td>
<td><p>查找子项目的项目的完整名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543870" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindItemByName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543870)"><strong>IWiaDrvItem::FindItemByName</strong></a></p></td>
<td><p>按项目的完整名称定位项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543873" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetDeviceSpecContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543873)"><strong>IWiaDrvItem::GetDeviceSpecContext</strong></a></p></td>
<td><p>检索一个指向特定于设备的上下文。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543878" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFirstChildItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543878)"><strong>IWiaDrvItem::GetFirstChildItem</strong></a></p></td>
<td><p>返回此文件夹项的第一个子级。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543881" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFullItemName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543881)"><strong>IWiaDrvItem::GetFullItemName</strong></a></p></td>
<td><p>检索项的完整名称和层次结构信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543883" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemFlags&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543883)"><strong>IWiaDrvItem::GetItemFlags</strong></a></p></td>
<td><p>返回 WIA 项标志。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543885" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543885)"><strong>IWiaDrvItem::GetItemName</strong></a></p></td>
<td><p>检索的项名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543889" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetNextSiblingItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543889)"><strong>IWiaDrvItem::GetNextSiblingItem</strong></a></p></td>
<td><p>查找此项的下一个同级。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543892" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetParentItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543892)"><strong>IWiaDrvItem::GetParentItem</strong></a></p></td>
<td><p>检索此项的父项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543899" data-raw-source="[&lt;strong&gt;IWiaDrvItem::RemoveItemFromFolder&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543899)"><strong>IWiaDrvItem::RemoveItemFromFolder</strong></a></p></td>
<td><p>从父文件夹中移除的项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543901" data-raw-source="[&lt;strong&gt;IWiaDrvItem::UnlinkItemTree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543901)"><strong>IWiaDrvItem::UnlinkItemTree</strong></a></p></td>
<td><p>取消驱动程序项树的链接。</p></td>
</tr>
</tbody>
</table>

 

 

 




