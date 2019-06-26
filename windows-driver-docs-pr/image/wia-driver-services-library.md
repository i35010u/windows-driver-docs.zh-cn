---
title: WIA 驱动程序服务库
ms.assetid: c179483b-74c3-4788-aa04-20cec0e0eb3a
description: 描述包含 WIA 微型驱动程序可以调用以获取帮助中执行特定任务的函数将 WIA 驱动程序服务库
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec4f2411140ffd27072ac9d481ae9dbf16600ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383753"
---
# <a name="wia-driver-services-library"></a>WIA 驱动程序服务库


WIA 驱动程序服务库包含 WIA 微型驱动程序可以调用以获取帮助中执行以下任务的函数：

-   [构建和维护项树](#ddk-building-and-maintaining-an-item-tree-si)
-   [日志记录错误和跟踪消息](#ddk-logging-error-and-trace-messages-si)
-   [读取和存储项的属性](#ddk-reading-and-storing-an-item-s-properties-si)
-   [更新并将数据传输](#ddk-updating-and-transferring-data-si)

WIA 微型驱动程序调用其中的大多数功能从其[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)方法根据需要。 每个 WIA 微型驱动程序，但是，必须调用[ **wiasCreateDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)函数，在[ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法创建驱动程序项目。 每次成功调用**wiasCreateDrvItem**函数创建**IWiaDrvItem**项对象，用于微型驱动程序的项目树中。 多个[IWiaDrvItem 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)方法具有类型的参数**IWiaDrvItem**，其中包括[ **IWiaDrvItem::AddItemToFolder** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)， [ **IWiaDrvItem::GetFirstChildItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem)， [ **IWiaDrvItem::GetNextSiblingItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem)，以及[ **IWiaDrvItem::GetParentItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem)。 此外， [ **wiasGetDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem)函数具有此类型的参数。

驱动程序服务库提供了以下函数。

## <a href="" id="ddk-building-and-maintaining-an-item-tree-si"></a>构建和维护项树


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatechildappitem" data-raw-source="[&lt;strong&gt;wiasCreateChildAppItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatechildappitem)"><strong>wiasCreateChildAppItem</strong></a></p></td>
<td><p>创建新的应用程序项目并将其作为指定的 （父） 项的子级。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem" data-raw-source="[&lt;strong&gt;wiasCreateDrvItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)"><strong>wiasCreateDrvItem</strong></a></p></td>
<td><p>创建<strong>IWiaDrvItem</strong>对象。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchildrencontexts" data-raw-source="[&lt;strong&gt;wiasGetChildrenContexts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchildrencontexts)"><strong>wiasGetChildrenContexts</strong></a></p></td>
<td><p>检索属于当前项的子级的项上下文的数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetcontextfromname" data-raw-source="[&lt;strong&gt;wiasGetContextFromName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetcontextfromname)"><strong>wiasGetContextFromName</strong></a></p></td>
<td><p>检索项名称的项上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem" data-raw-source="[&lt;strong&gt;wiasGetDrvItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem)"><strong>wiasGetDrvItem</strong></a></p></td>
<td><p>检索驱动程序项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetrootitem" data-raw-source="[&lt;strong&gt;wiasGetRootItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetrootitem)"><strong>wiasGetRootItem</strong></a></p></td>
<td><p>检索指定的 WIA 项的根项上下文。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-logging-error-and-trace-messages-si"></a>日志记录错误和跟踪消息


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreateloginstance" data-raw-source="[&lt;strong&gt;wiasCreateLogInstance&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreateloginstance)"><strong>wiasCreateLogInstance</strong></a></p></td>
<td><p>创建日志记录对象的实例。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugerror" data-raw-source="[&lt;strong&gt;wiasDebugError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugerror)"><strong>wiasDebugError</strong></a></p></td>
<td><p>打印设备管理器调试控制台中的调试错误字符串。 始终输出颜色为红色。 此函数仅用于兼容性提供。 在 Microsoft Windows XP 中，建议使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lerror" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lerror)"> <strong>WIAS_LERROR</strong> </a>相反。</p>
<p>在 Windows Vista 中，建议使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_error" data-raw-source="[&lt;strong&gt;WIAS_ERROR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_error)"> <strong>WIAS_ERROR</strong> </a>相反。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugtrace" data-raw-source="[&lt;strong&gt;wiasDebugTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugtrace)"><strong>wiasDebugTrace</strong></a></p></td>
<td><p>打印设备管理器调试控制台中的调试跟踪字符串。 此函数仅用于兼容性提供。 在 Microsoft Windows XP 中，建议使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_ltrace" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_ltrace)"> <strong>WIAS_LTRACE</strong> </a>相反。</p>
<p>在 Windows Vista 中，建议使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_trace" data-raw-source="[&lt;strong&gt;WIA_TRACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_trace)"> <strong>WIA_TRACE</strong> </a>相反。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasformatargs" data-raw-source="[&lt;strong&gt;wiasFormatArgs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasformatargs)"><strong>wiasFormatArgs</strong></a></p></td>
<td><p>参数列表的格式设置为日志记录的打包字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasprintdebughresult" data-raw-source="[&lt;strong&gt;wiasPrintDebugHResult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasprintdebughresult)"><strong>wiasPrintDebugHResult</strong></a></p></td>
<td><p>设备管理器调试控制台上打印 HRESULT 字符串。 此函数仅用于兼容性提供。 它是已过时的 Windows XP 及更高版本，并不再受支持。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lhresult" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lhresult)"> <strong>WIAS_LHRESULT</strong> </a>相反。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-reading-and-storing-an-item-s-properties-si"></a>读取和存储项的属性


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext" data-raw-source="[&lt;strong&gt;wiasCreatePropContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)"><strong>wiasCreatePropContext</strong></a></p></td>
<td><p>分配属性上下文，以指示该项目的属性更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasfreepropcontext" data-raw-source="[&lt;strong&gt;wiasFreePropContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasfreepropcontext)"><strong>wiasFreePropContext</strong></a></p></td>
<td><p>释放所占用的内存<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_context" data-raw-source="[&lt;strong&gt;WIA_PROPERTY_CONTEXT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)"> <strong>WIA_PROPERTY_CONTEXT</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat" data-raw-source="[&lt;strong&gt;wiasGetChangedValueFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)"><strong>wiasGetChangedValueFloat</strong></a></p></td>
<td><p>确定是否已由应用程序更改具有浮点值的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvalueguid" data-raw-source="[&lt;strong&gt;wiasGetChangedValueGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)"><strong>wiasGetChangedValueGuid</strong></a></p></td>
<td><p>确定是否已由应用程序更改具有 GUID 值的属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluelong" data-raw-source="[&lt;strong&gt;wiasGetChangedValueLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)"><strong>wiasGetChangedValueLong</strong></a></p></td>
<td><p>确定是否已由应用程序更改包含长整型值的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluestr" data-raw-source="[&lt;strong&gt;wiasGetChangedValueStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)"><strong>wiasGetChangedValueStr</strong></a></p></td>
<td><p>确定是否已由应用程序更改具有字符串值的属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetitemtype" data-raw-source="[&lt;strong&gt;wiasGetItemType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetitemtype)"><strong>wiasGetItemType</strong></a></p></td>
<td><p>表示根或子项目。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasGetPropertyAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetpropertyattributes)"><strong>wiasGetPropertyAttributes</strong></a></p></td>
<td><p>检索访问标志和一组属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasispropchanged" data-raw-source="[&lt;strong&gt;wiasIsPropChanged&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasispropchanged)"><strong>wiasIsPropChanged</strong></a></p></td>
<td><p>测试是否已由应用程序更改指定的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadmultiple" data-raw-source="[&lt;strong&gt;wiasReadMultiple&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadmultiple)"><strong>wiasReadMultiple</strong></a></p></td>
<td><p>从 WIA 项中读取多个属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropbin" data-raw-source="[&lt;strong&gt;wiasReadPropBin&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropbin)"><strong>wiasReadPropBin</strong></a></p></td>
<td><p>从 WIA 项中读取单个二进制属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropfloat" data-raw-source="[&lt;strong&gt;wiasReadPropFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropfloat)"><strong>wiasReadPropFloat</strong></a></p></td>
<td><p>从 WIA 项检索浮点属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropguid" data-raw-source="[&lt;strong&gt;wiasReadPropGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropguid)"><strong>wiasReadPropGuid</strong></a></p></td>
<td><p>检索从 WIA 项的 GUID 属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong" data-raw-source="[&lt;strong&gt;wiasReadPropLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong)"><strong>wiasReadPropLong</strong></a></p></td>
<td><p>从 WIA 项检索长整型属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropstr" data-raw-source="[&lt;strong&gt;wiasReadPropStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropstr)"><strong>wiasReadPropStr</strong></a></p></td>
<td><p>检索从 WIA 项字符串属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropattribs" data-raw-source="[&lt;strong&gt;wiasSetItemPropAttribs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropattribs)"><strong>wiasSetItemPropAttribs</strong></a></p></td>
<td><p>设置访问标志和有效的项的组属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropnames" data-raw-source="[&lt;strong&gt;wiasSetItemPropNames&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropnames)"><strong>wiasSetItemPropNames</strong></a></p></td>
<td><p>写入项属性的属性名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropchanged" data-raw-source="[&lt;strong&gt;wiasSetPropChanged&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropchanged)"><strong>wiasSetPropChanged</strong></a></p></td>
<td><p>修改属性上下文，以指示更改属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasSetPropertyAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropertyattributes)"><strong>wiasSetPropertyAttributes</strong></a></p></td>
<td><p>设置访问标志和项的属性的属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidflag" data-raw-source="[&lt;strong&gt;wiasSetValidFlag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidflag)"><strong>wiasSetValidFlag</strong></a></p></td>
<td><p>设置 WIA_PROP_FLAG 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistfloat" data-raw-source="[&lt;strong&gt;wiasSetValidListFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistfloat)"><strong>wiasSetValidListFloat</strong></a></p></td>
<td><p>设置类型子 VT_R4 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistguid" data-raw-source="[&lt;strong&gt;wiasSetValidListGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistguid)"><strong>wiasSetValidListGuid</strong></a></p></td>
<td><p>设置的子类型 VT_CLSID WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistlong" data-raw-source="[&lt;strong&gt;wiasSetValidListLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistlong)"><strong>wiasSetValidListLong</strong></a></p></td>
<td><p>设置类型子 VT_I4 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidliststr" data-raw-source="[&lt;strong&gt;wiasSetValidListStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidliststr)"><strong>wiasSetValidListStr</strong></a></p></td>
<td><p>设置类型子 VT_BSTR WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangefloat" data-raw-source="[&lt;strong&gt;wiasSetValidRangeFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangefloat)"><strong>wiasSetValidRangeFloat</strong></a></p></td>
<td><p>指定子类型 VT_R4 WIA_PROP_RANGE 属性的有效值的范围。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangelong" data-raw-source="[&lt;strong&gt;wiasSetValidRangeLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangelong)"><strong>wiasSetValidRangeLong</strong></a></p></td>
<td><p>指定子类型 VT_I4 WIA_PROP_RANGE 属性的有效值的范围。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatevalidformat" data-raw-source="[&lt;strong&gt;wiasUpdateValidFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatevalidformat)"><strong>wiasUpdateValidFormat</strong></a></p></td>
<td><p>为当前的微型驱动程序更新属性上下文的有效格式。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties" data-raw-source="[&lt;strong&gt;wiasValidateItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties)"><strong>wiasValidateItemProperties</strong></a></p></td>
<td><p>验证针对其当前有效的值的简单项属性的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple" data-raw-source="[&lt;strong&gt;wiasWriteMultiple&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)"><strong>wiasWriteMultiple</strong></a></p></td>
<td><p>将多个属性值写入到 WIA 项 （不同类型的可能是属性）。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropbin" data-raw-source="[&lt;strong&gt;wiasWritePropBin&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropbin)"><strong>wiasWritePropBin</strong></a></p></td>
<td><p>将一个单一的二进制属性值写入到 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropfloat" data-raw-source="[&lt;strong&gt;wiasWritePropFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropfloat)"><strong>wiasWritePropFloat</strong></a></p></td>
<td><p>将浮点属性值写入到 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropguid" data-raw-source="[&lt;strong&gt;wiasWritePropGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropguid)"><strong>wiasWritePropGuid</strong></a></p></td>
<td><p>将 GUID 属性值写入到 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswriteproplong" data-raw-source="[&lt;strong&gt;wiasWritePropLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswriteproplong)"><strong>wiasWritePropLong</strong></a></p></td>
<td><p>将长整数属性值写入到 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropstr" data-raw-source="[&lt;strong&gt;wiasWritePropStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropstr)"><strong>wiasWritePropStr</strong></a></p></td>
<td><p>将字符串属性值写入到 WIA 项。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-updating-and-transferring-data-si"></a>更新并将数据传输


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdownsamplebuffer" data-raw-source="[&lt;strong&gt;wiasDownSampleBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdownsamplebuffer)"><strong>wiasDownSampleBuffer</strong></a></p></td>
<td><p>将像素数据和缩减像素采样的缓冲区中指定的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetimageinformation" data-raw-source="[&lt;strong&gt;wiasGetImageInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetimageinformation)"><strong>wiasGetImageInformation</strong></a></p></td>
<td><p>检索从一个项中传输上下文信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasparseendorserstring" data-raw-source="[&lt;strong&gt;wiasParseEndorserString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasparseendorserstring)"><strong>wiasParseEndorserString</strong></a></p></td>
<td><p>分析印记签署器字符串，WIA 服务定义和供应商定义字符串中的标记替换为与令牌相关联的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassendendofpage" data-raw-source="[&lt;strong&gt;wiasSendEndOfPage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassendendofpage)"><strong>wiasSendEndOfPage</strong></a></p></td>
<td><p>在数据传输，发送的当前总页计数的过程调用的客户端回调例程。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatescanrect" data-raw-source="[&lt;strong&gt;wiasUpdateScanRect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatescanrect)"><strong>wiasUpdateScanRect</strong></a></p></td>
<td><p>更新扫描设备的扫描区域大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritebuftofile" data-raw-source="[&lt;strong&gt;wiasWriteBufToFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritebuftofile)"><strong>wiasWriteBufToFile</strong></a></p></td>
<td><p>将临时页缓冲区的内容写入到图像文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepagebuftofile" data-raw-source="[&lt;strong&gt;wiasWritePageBufToFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepagebuftofile)"><strong>wiasWritePageBufToFile</strong></a></p></td>
<td><p>将临时页缓冲区的内容写入到图像文件。 使用此函数将页面写入多页 TIFF 文件。</p></td>
</tr>
</tbody>
</table>

 

 

 




