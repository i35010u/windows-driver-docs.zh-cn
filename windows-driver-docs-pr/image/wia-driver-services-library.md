---
title: WIA 驱动程序服务库
ms.assetid: c179483b-74c3-4788-aa04-20cec0e0eb3a
description: 介绍 WIA 驱动程序服务库，其中包含 WIA 微型驱动程序可以为执行特定任务而调用的帮助
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d9416395671e76493879c30073a94a97d7177ce
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105596"
---
# <a name="wia-driver-services-library"></a>WIA 驱动程序服务库


WIA 驱动程序服务库包含 WIA 微型驱动程序在执行以下任务时可以调用的函数：

-   [生成和维护项树](#ddk-building-and-maintaining-an-item-tree-si)
-   [记录错误和跟踪消息](#ddk-logging-error-and-trace-messages-si)
-   [读取和存储项的属性](#ddk-reading-and-storing-an-item-s-properties-si)
-   [更新和传输数据](#ddk-updating-and-transferring-data-si)

WIA 微型驱动程序根据需要从其 [IWiaMiniDrv 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv) 方法调用大多数这些函数。 但是，每个 WIA 微型驱动程序都必须调用[**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法中的[**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)函数来创建驱动程序项。 对 **wiasCreateDrvItem** 函数的每个成功调用都将创建一个 **IWiaDrvItem** 项对象，该对象在微型驱动程序的项树中使用。 多 [个 IWiaDrvItem 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem) 方法具有类型为 **IWiaDrvItem**的参数，其中包括 [**IWiaDrvItem：： AddItemToFolder**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)、 [**IWiaDrvItem：： GetFirstChildItem**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem)、 [**IWiaDrvItem：： GetNextSiblingItem**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem)和 [**IWiaDrvItem：： GetParentItem**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem)。 此外， [**wiasGetDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem) 函数有一个此类型的参数。

驱动程序服务库提供了以下功能。

## <a name="building-and-maintaining-an-item-tree"></a><a href="" id="ddk-building-and-maintaining-an-item-tree-si"></a>生成和维护项树


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem" data-raw-source="[&lt;strong&gt;wiasCreateChildAppItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem)"><strong>wiasCreateChildAppItem</strong></a></p></td>
<td><p>创建一个新的应用程序项，并将其作为指定 (父) 项的子级插入。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem" data-raw-source="[&lt;strong&gt;wiasCreateDrvItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)"><strong>wiasCreateDrvItem</strong></a></p></td>
<td><p>创建 <strong>IWiaDrvItem</strong> 对象。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchildrencontexts" data-raw-source="[&lt;strong&gt;wiasGetChildrenContexts&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchildrencontexts)"><strong>wiasGetChildrenContexts</strong></a></p></td>
<td><p>检索属于当前项的子项的项上下文的数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetcontextfromname" data-raw-source="[&lt;strong&gt;wiasGetContextFromName&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetcontextfromname)"><strong>wiasGetContextFromName</strong></a></p></td>
<td><p>检索项名称的项上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem" data-raw-source="[&lt;strong&gt;wiasGetDrvItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem)"><strong>wiasGetDrvItem</strong></a></p></td>
<td><p>检索驱动程序项。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetrootitem" data-raw-source="[&lt;strong&gt;wiasGetRootItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetrootitem)"><strong>wiasGetRootItem</strong></a></p></td>
<td><p>检索指定 WIA 项的根项上下文。</p></td>
</tr>
</tbody>
</table>

 

## <a name="logging-error-and-trace-messages"></a><a href="" id="ddk-logging-error-and-trace-messages-si"></a>记录错误和跟踪消息


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreateloginstance" data-raw-source="[&lt;strong&gt;wiasCreateLogInstance&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreateloginstance)"><strong>wiasCreateLogInstance</strong></a></p></td>
<td><p>创建日志记录对象的实例。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugerror" data-raw-source="[&lt;strong&gt;wiasDebugError&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugerror)"><strong>wiasDebugError</strong></a></p></td>
<td><p>在设备管理器调试控制台中打印调试错误字符串。 输出颜色始终为红色。 提供此函数只是为了实现兼容性。 在 Microsoft Windows XP 中，建议改用 <a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror)"><strong>WIAS_LERROR</strong></a> 。</p>
<p>在 Windows Vista 中，建议改用 <a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error" data-raw-source="[&lt;strong&gt;WIAS_ERROR&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error)"><strong>WIAS_ERROR</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugtrace" data-raw-source="[&lt;strong&gt;wiasDebugTrace&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugtrace)"><strong>wiasDebugTrace</strong></a></p></td>
<td><p>在设备管理器调试控制台中打印调试跟踪字符串。 提供此函数只是为了实现兼容性。 在 Microsoft Windows XP 中，建议改用 <a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace)"><strong>WIAS_LTRACE</strong></a> 。</p>
<p>在 Windows Vista 中，建议改用 <a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace" data-raw-source="[&lt;strong&gt;WIA_TRACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace)"><strong>WIA_TRACE</strong></a> 。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasformatargs" data-raw-source="[&lt;strong&gt;wiasFormatArgs&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasformatargs)"><strong>wiasFormatArgs</strong></a></p></td>
<td><p>将参数列表的格式设置为打包字符串以进行日志记录。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasprintdebughresult" data-raw-source="[&lt;strong&gt;wiasPrintDebugHResult&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasprintdebughresult)"><strong>wiasPrintDebugHResult</strong></a></p></td>
<td><p>在设备管理器调试控制台上打印 HRESULT 字符串。 提供此函数只是为了实现兼容性。 它在 Windows XP 及更高版本中已过时，不再受支持。 改用 <a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult)"><strong>WIAS_LHRESULT</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

## <a name="reading-and-storing-an-items-properties"></a><a href="" id="ddk-reading-and-storing-an-item-s-properties-si"></a>读取和存储项的属性


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext" data-raw-source="[&lt;strong&gt;wiasCreatePropContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)"><strong>wiasCreatePropContext</strong></a></p></td>
<td><p>分配属性上下文以指示要更改的项的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext" data-raw-source="[&lt;strong&gt;wiasFreePropContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext)"><strong>wiasFreePropContext</strong></a></p></td>
<td><p>释放 <a href="/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context" data-raw-source="[&lt;strong&gt;WIA_PROPERTY_CONTEXT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)"><strong>WIA_PROPERTY_CONTEXT</strong></a> 结构占用的内存。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat" data-raw-source="[&lt;strong&gt;wiasGetChangedValueFloat&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)"><strong>wiasGetChangedValueFloat</strong></a></p></td>
<td><p>确定具有浮点值的属性是否已由应用程序更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid" data-raw-source="[&lt;strong&gt;wiasGetChangedValueGuid&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)"><strong>wiasGetChangedValueGuid</strong></a></p></td>
<td><p>确定具有 GUID 值的属性是否已由应用程序更改。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong" data-raw-source="[&lt;strong&gt;wiasGetChangedValueLong&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)"><strong>wiasGetChangedValueLong</strong></a></p></td>
<td><p>确定具有长整数值的属性是否已由应用程序更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr" data-raw-source="[&lt;strong&gt;wiasGetChangedValueStr&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)"><strong>wiasGetChangedValueStr</strong></a></p></td>
<td><p>确定具有字符串值的属性是否已由应用程序更改。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetitemtype" data-raw-source="[&lt;strong&gt;wiasGetItemType&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetitemtype)"><strong>wiasGetItemType</strong></a></p></td>
<td><p>指示根项或子项。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasGetPropertyAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes)"><strong>wiasGetPropertyAttributes</strong></a></p></td>
<td><p>检索一组属性的访问标志和有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasispropchanged" data-raw-source="[&lt;strong&gt;wiasIsPropChanged&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasispropchanged)"><strong>wiasIsPropChanged</strong></a></p></td>
<td><p>测试指定的属性是否已由应用程序更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple" data-raw-source="[&lt;strong&gt;wiasReadMultiple&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple)"><strong>wiasReadMultiple</strong></a></p></td>
<td><p>从 WIA 项读取多个属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin" data-raw-source="[&lt;strong&gt;wiasReadPropBin&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin)"><strong>wiasReadPropBin</strong></a></p></td>
<td><p>从 WIA 项读取单个二进制属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat" data-raw-source="[&lt;strong&gt;wiasReadPropFloat&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat)"><strong>wiasReadPropFloat</strong></a></p></td>
<td><p>从 WIA 项中检索浮点属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid" data-raw-source="[&lt;strong&gt;wiasReadPropGuid&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid)"><strong>wiasReadPropGuid</strong></a></p></td>
<td><p>从 WIA 项检索 GUID 属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong" data-raw-source="[&lt;strong&gt;wiasReadPropLong&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)"><strong>wiasReadPropLong</strong></a></p></td>
<td><p>检索 WIA 项中的长整型属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr" data-raw-source="[&lt;strong&gt;wiasReadPropStr&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr)"><strong>wiasReadPropStr</strong></a></p></td>
<td><p>从 WIA 项中检索字符串属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropattribs" data-raw-source="[&lt;strong&gt;wiasSetItemPropAttribs&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropattribs)"><strong>wiasSetItemPropAttribs</strong></a></p></td>
<td><p>为项的一组属性设置访问标志和有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropnames" data-raw-source="[&lt;strong&gt;wiasSetItemPropNames&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropnames)"><strong>wiasSetItemPropNames</strong></a></p></td>
<td><p>将属性名称写入项属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropchanged" data-raw-source="[&lt;strong&gt;wiasSetPropChanged&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropchanged)"><strong>wiasSetPropChanged</strong></a></p></td>
<td><p>修改属性上下文以指示属性正在更改。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasSetPropertyAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropertyattributes)"><strong>wiasSetPropertyAttributes</strong></a></p></td>
<td><p>设置项属性的访问标志和属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidflag" data-raw-source="[&lt;strong&gt;wiasSetValidFlag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidflag)"><strong>wiasSetValidFlag</strong></a></p></td>
<td><p>设置 WIA_PROP_FLAG 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistfloat" data-raw-source="[&lt;strong&gt;wiasSetValidListFloat&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistfloat)"><strong>wiasSetValidListFloat</strong></a></p></td>
<td><p>设置 VT_R4 子类型的 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistguid" data-raw-source="[&lt;strong&gt;wiasSetValidListGuid&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistguid)"><strong>wiasSetValidListGuid</strong></a></p></td>
<td><p>设置子类型 VT_CLSID 的 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistlong" data-raw-source="[&lt;strong&gt;wiasSetValidListLong&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistlong)"><strong>wiasSetValidListLong</strong></a></p></td>
<td><p>设置 VT_I4 子类型的 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidliststr" data-raw-source="[&lt;strong&gt;wiasSetValidListStr&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidliststr)"><strong>wiasSetValidListStr</strong></a></p></td>
<td><p>设置 VT_BSTR 子类型的 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangefloat" data-raw-source="[&lt;strong&gt;wiasSetValidRangeFloat&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangefloat)"><strong>wiasSetValidRangeFloat</strong></a></p></td>
<td><p>指定子类型 VT_R4 的 WIA_PROP_RANGE 属性的有效值范围。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangelong" data-raw-source="[&lt;strong&gt;wiasSetValidRangeLong&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangelong)"><strong>wiasSetValidRangeLong</strong></a></p></td>
<td><p>指定子类型 VT_I4 的 WIA_PROP_RANGE 属性的有效值范围。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatevalidformat" data-raw-source="[&lt;strong&gt;wiasUpdateValidFormat&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatevalidformat)"><strong>wiasUpdateValidFormat</strong></a></p></td>
<td><p>更新当前微型驱动程序的属性上下文的有效格式。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties" data-raw-source="[&lt;strong&gt;wiasValidateItemProperties&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties)"><strong>wiasValidateItemProperties</strong></a></p></td>
<td><p>根据其当前有效值验证简单项属性的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple" data-raw-source="[&lt;strong&gt;wiasWriteMultiple&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)"><strong>wiasWriteMultiple</strong></a></p></td>
<td><p>向 WIA 项写入多个属性值 (属性可能属于不同类型) 。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin" data-raw-source="[&lt;strong&gt;wiasWritePropBin&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin)"><strong>wiasWritePropBin</strong></a></p></td>
<td><p>向 WIA 项写入一个二进制属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat" data-raw-source="[&lt;strong&gt;wiasWritePropFloat&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat)"><strong>wiasWritePropFloat</strong></a></p></td>
<td><p>将浮点属性值写入 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid" data-raw-source="[&lt;strong&gt;wiasWritePropGuid&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid)"><strong>wiasWritePropGuid</strong></a></p></td>
<td><p>将 GUID 属性值写入 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong" data-raw-source="[&lt;strong&gt;wiasWritePropLong&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong)"><strong>wiasWritePropLong</strong></a></p></td>
<td><p>向 WIA 项写入一个长整型属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr" data-raw-source="[&lt;strong&gt;wiasWritePropStr&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr)"><strong>wiasWritePropStr</strong></a></p></td>
<td><p>向 WIA 项写入一个字符串属性值。</p></td>
</tr>
</tbody>
</table>

 

## <a name="updating-and-transferring-data"></a><a href="" id="ddk-updating-and-transferring-data-si"></a>更新和传输数据


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdownsamplebuffer" data-raw-source="[&lt;strong&gt;wiasDownSampleBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdownsamplebuffer)"><strong>wiasDownSampleBuffer</strong></a></p></td>
<td><p>采用一个像素数据缓冲区，并将其 downsamples 为指定的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation" data-raw-source="[&lt;strong&gt;wiasGetImageInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation)"><strong>wiasGetImageInformation</strong></a></p></td>
<td><p>从项中检索传输上下文信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasparseendorserstring" data-raw-source="[&lt;strong&gt;wiasParseEndorserString&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasparseendorserstring)"><strong>wiasParseEndorserString</strong></a></p></td>
<td><p>分析 endorser 字符串，并将字符串中的 WIA 服务定义和供应商定义的标记替换为与标记相关联的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage" data-raw-source="[&lt;strong&gt;wiasSendEndOfPage&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage)"><strong>wiasSendEndOfPage</strong></a></p></td>
<td><p>在数据传输过程中调用客户端回调例程，并发送当前总页数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatescanrect" data-raw-source="[&lt;strong&gt;wiasUpdateScanRect&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatescanrect)"><strong>wiasUpdateScanRect</strong></a></p></td>
<td><p>更新扫描设备的扫描区域大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritebuftofile" data-raw-source="[&lt;strong&gt;wiasWriteBufToFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritebuftofile)"><strong>wiasWriteBufToFile</strong></a></p></td>
<td><p>将临时页缓冲区的内容写入映像文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepagebuftofile" data-raw-source="[&lt;strong&gt;wiasWritePageBufToFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepagebuftofile)"><strong>wiasWritePageBufToFile</strong></a></p></td>
<td><p>将临时页缓冲区的内容写入映像文件。 使用此函数可将页面写入多页面 TIFF 文件。</p></td>
</tr>
</tbody>
</table>

 

