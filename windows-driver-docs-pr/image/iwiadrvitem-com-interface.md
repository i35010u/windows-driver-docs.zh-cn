---
title: IWiaDrvItem COM 接口
description: IWiaDrvItem COM 接口
ms.assetid: 1be2265b-7ae8-4935-9559-588b885526d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5264995c7d22c340da474bfb463c08c09b3a1b61
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188319"
---
# <a name="iwiadrvitem-com-interface"></a>IWiaDrvItem COM 接口





[IWiaDrvItem 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)提供了 WIA 微型驱动程序用于管理**IWiaDrvItem**项树的方法。 这些方法允许 WIA 微型驱动程序操作 **IWiaDrvItem** 对象。 **IWiaDrvItem**接口提供以下方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder" data-raw-source="[&lt;strong&gt;IWiaDrvItem::AddItemToFolder&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)"><strong>IWiaDrvItem::AddItemToFolder</strong></a></p></td>
<td><p>将 <strong>IWiaDrvItem</strong> 对象添加到文件夹。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-dumpitemdata" data-raw-source="[&lt;strong&gt;IWiaDrvItem::DumpItemData&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-dumpitemdata)"><strong>IWiaDrvItem：:D umpItemData</strong></a></p></td>
<td><p>转储私有驱动程序项数据。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-findchilditembyname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindChildItemByName&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-findchilditembyname)"><strong>IWiaDrvItem::FindChildItemByName</strong></a></p></td>
<td><p>按完整项名称定位子项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-finditembyname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindItemByName&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-finditembyname)"><strong>IWiaDrvItem::FindItemByName</strong></a></p></td>
<td><p>按完整项名称查找项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getdevicespeccontext" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetDeviceSpecContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getdevicespeccontext)"><strong>IWiaDrvItem::GetDeviceSpecContext</strong></a></p></td>
<td><p>检索指向设备特定上下文的指针。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFirstChildItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem)"><strong>IWiaDrvItem::GetFirstChildItem</strong></a></p></td>
<td><p>返回此文件夹项的第一个子级。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfullitemname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFullItemName&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfullitemname)"><strong>IWiaDrvItem::GetFullItemName</strong></a></p></td>
<td><p>检索项的完整名称和层次结构信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemFlags&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags)"><strong>IWiaDrvItem::GetItemFlags</strong></a></p></td>
<td><p>返回 WIA 项标志。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemName&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemname)"><strong>IWiaDrvItem::GetItemName</strong></a></p></td>
<td><p>检索项的名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetNextSiblingItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem)"><strong>IWiaDrvItem::GetNextSiblingItem</strong></a></p></td>
<td><p>查找此项的下一个同级。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetParentItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem)"><strong>IWiaDrvItem::GetParentItem</strong></a></p></td>
<td><p>检索此项的父项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-removeitemfromfolder" data-raw-source="[&lt;strong&gt;IWiaDrvItem::RemoveItemFromFolder&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-removeitemfromfolder)"><strong>IWiaDrvItem::RemoveItemFromFolder</strong></a></p></td>
<td><p>从父文件夹中移除项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-unlinkitemtree" data-raw-source="[&lt;strong&gt;IWiaDrvItem::UnlinkItemTree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-unlinkitemtree)"><strong>IWiaDrvItem::UnlinkItemTree</strong></a></p></td>
<td><p>断开驱动程序项树。</p></td>
</tr>
</tbody>
</table>

 

 

