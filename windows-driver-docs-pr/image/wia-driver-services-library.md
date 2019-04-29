---
title: WIA 驱动程序服务库
ms.assetid: c179483b-74c3-4788-aa04-20cec0e0eb3a
description: 描述包含 WIA 微型驱动程序可以调用以获取帮助中执行特定任务的函数将 WIA 驱动程序服务库
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c966aa0a8563ae0ab2b62a38a39a6660642b51c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365980"
---
# <a name="wia-driver-services-library"></a>WIA 驱动程序服务库


WIA 驱动程序服务库包含 WIA 微型驱动程序可以调用以获取帮助中执行以下任务的函数：

-   [构建和维护项树](#ddk-building-and-maintaining-an-item-tree-si)
-   [日志记录错误和跟踪消息](#ddk-logging-error-and-trace-messages-si)
-   [读取和存储项的属性](#ddk-reading-and-storing-an-item-s-properties-si)
-   [更新并将数据传输](#ddk-updating-and-transferring-data-si)

WIA 微型驱动程序调用其中的大多数功能从其[IWiaMiniDrv 接口](https://msdn.microsoft.com/library/windows/hardware/ff545027)方法根据需要。 每个 WIA 微型驱动程序，但是，必须调用[ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)函数，在[ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)方法创建驱动程序项目。 每次成功调用**wiasCreateDrvItem**函数创建**IWiaDrvItem**项对象，用于微型驱动程序的项目树中。 多个[IWiaDrvItem 接口](https://msdn.microsoft.com/library/windows/hardware/ff543896)方法具有类型的参数**IWiaDrvItem**，其中包括[ **IWiaDrvItem::AddItemToFolder** ](https://msdn.microsoft.com/library/windows/hardware/ff543856)， [ **IWiaDrvItem::GetFirstChildItem**](https://msdn.microsoft.com/library/windows/hardware/ff543878)， [ **IWiaDrvItem::GetNextSiblingItem**](https://msdn.microsoft.com/library/windows/hardware/ff543889)，以及[ **IWiaDrvItem::GetParentItem**](https://msdn.microsoft.com/library/windows/hardware/ff543892)。 此外， [ **wiasGetDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549243)函数具有此类型的参数。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549156" data-raw-source="[&lt;strong&gt;wiasCreateChildAppItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549156)"><strong>wiasCreateChildAppItem</strong></a></p></td>
<td><p>创建新的应用程序项目并将其作为指定的 （父） 项的子级。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549160" data-raw-source="[&lt;strong&gt;wiasCreateDrvItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549160)"><strong>wiasCreateDrvItem</strong></a></p></td>
<td><p>创建<strong>IWiaDrvItem</strong>对象。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549224" data-raw-source="[&lt;strong&gt;wiasGetChildrenContexts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549224)"><strong>wiasGetChildrenContexts</strong></a></p></td>
<td><p>检索属于当前项的子级的项上下文的数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549233" data-raw-source="[&lt;strong&gt;wiasGetContextFromName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549233)"><strong>wiasGetContextFromName</strong></a></p></td>
<td><p>检索项名称的项上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549243" data-raw-source="[&lt;strong&gt;wiasGetDrvItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549243)"><strong>wiasGetDrvItem</strong></a></p></td>
<td><p>检索驱动程序项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549264" data-raw-source="[&lt;strong&gt;wiasGetRootItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549264)"><strong>wiasGetRootItem</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549163" data-raw-source="[&lt;strong&gt;wiasCreateLogInstance&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549163)"><strong>wiasCreateLogInstance</strong></a></p></td>
<td><p>创建日志记录对象的实例。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549170" data-raw-source="[&lt;strong&gt;wiasDebugError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549170)"><strong>wiasDebugError</strong></a></p></td>
<td><p>打印设备管理器调试控制台中的调试错误字符串。 始终输出颜色为红色。 此函数仅用于兼容性提供。 在 Microsoft Windows XP 中，建议使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549580" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549580)"> <strong>WIAS_LERROR</strong> </a>相反。</p>
<p>在 Windows Vista 中，建议使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549565" data-raw-source="[&lt;strong&gt;WIAS_ERROR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549565)"> <strong>WIAS_ERROR</strong> </a>相反。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549178" data-raw-source="[&lt;strong&gt;wiasDebugTrace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549178)"><strong>wiasDebugTrace</strong></a></p></td>
<td><p>打印设备管理器调试控制台中的调试跟踪字符串。 此函数仅用于兼容性提供。 在 Microsoft Windows XP 中，建议使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549600" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549600)"> <strong>WIAS_LTRACE</strong> </a>相反。</p>
<p>在 Windows Vista 中，建议使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549619" data-raw-source="[&lt;strong&gt;WIA_TRACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549619)"> <strong>WIA_TRACE</strong> </a>相反。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549190" data-raw-source="[&lt;strong&gt;wiasFormatArgs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549190)"><strong>wiasFormatArgs</strong></a></p></td>
<td><p>参数列表的格式设置为日志记录的打包字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549287" data-raw-source="[&lt;strong&gt;wiasPrintDebugHResult&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549287)"><strong>wiasPrintDebugHResult</strong></a></p></td>
<td><p>设备管理器调试控制台上打印 HRESULT 字符串。 此函数仅用于兼容性提供。 它是已过时的 Windows XP 及更高版本，并不再受支持。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549589" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549589)"> <strong>WIAS_LHRESULT</strong> </a>相反。</p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549167" data-raw-source="[&lt;strong&gt;wiasCreatePropContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549167)"><strong>wiasCreatePropContext</strong></a></p></td>
<td><p>分配属性上下文，以指示该项目的属性更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549195" data-raw-source="[&lt;strong&gt;wiasFreePropContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549195)"><strong>wiasFreePropContext</strong></a></p></td>
<td><p>释放所占用的内存<a href="https://msdn.microsoft.com/library/windows/hardware/ff552749" data-raw-source="[&lt;strong&gt;WIA_PROPERTY_CONTEXT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552749)"> <strong>WIA_PROPERTY_CONTEXT</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549200" data-raw-source="[&lt;strong&gt;wiasGetChangedValueFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549200)"><strong>wiasGetChangedValueFloat</strong></a></p></td>
<td><p>确定是否已由应用程序更改具有浮点值的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549211" data-raw-source="[&lt;strong&gt;wiasGetChangedValueGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549211)"><strong>wiasGetChangedValueGuid</strong></a></p></td>
<td><p>确定是否已由应用程序更改具有 GUID 值的属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549214" data-raw-source="[&lt;strong&gt;wiasGetChangedValueLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549214)"><strong>wiasGetChangedValueLong</strong></a></p></td>
<td><p>确定是否已由应用程序更改包含长整型值的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549219" data-raw-source="[&lt;strong&gt;wiasGetChangedValueStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549219)"><strong>wiasGetChangedValueStr</strong></a></p></td>
<td><p>确定是否已由应用程序更改具有字符串值的属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549255" data-raw-source="[&lt;strong&gt;wiasGetItemType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549255)"><strong>wiasGetItemType</strong></a></p></td>
<td><p>表示根或子项目。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549257" data-raw-source="[&lt;strong&gt;wiasGetPropertyAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549257)"><strong>wiasGetPropertyAttributes</strong></a></p></td>
<td><p>检索访问标志和一组属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549271" data-raw-source="[&lt;strong&gt;wiasIsPropChanged&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549271)"><strong>wiasIsPropChanged</strong></a></p></td>
<td><p>测试是否已由应用程序更改指定的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549300" data-raw-source="[&lt;strong&gt;wiasReadMultiple&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549300)"><strong>wiasReadMultiple</strong></a></p></td>
<td><p>从 WIA 项中读取多个属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549308" data-raw-source="[&lt;strong&gt;wiasReadPropBin&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549308)"><strong>wiasReadPropBin</strong></a></p></td>
<td><p>从 WIA 项中读取单个二进制属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549320" data-raw-source="[&lt;strong&gt;wiasReadPropFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549320)"><strong>wiasReadPropFloat</strong></a></p></td>
<td><p>从 WIA 项检索浮点属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549325" data-raw-source="[&lt;strong&gt;wiasReadPropGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549325)"><strong>wiasReadPropGuid</strong></a></p></td>
<td><p>检索从 WIA 项的 GUID 属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549330" data-raw-source="[&lt;strong&gt;wiasReadPropLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549330)"><strong>wiasReadPropLong</strong></a></p></td>
<td><p>从 WIA 项检索长整型属性值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549341" data-raw-source="[&lt;strong&gt;wiasReadPropStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549341)"><strong>wiasReadPropStr</strong></a></p></td>
<td><p>检索从 WIA 项字符串属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549358" data-raw-source="[&lt;strong&gt;wiasSetItemPropAttribs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549358)"><strong>wiasSetItemPropAttribs</strong></a></p></td>
<td><p>设置访问标志和有效的项的组属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549369" data-raw-source="[&lt;strong&gt;wiasSetItemPropNames&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549369)"><strong>wiasSetItemPropNames</strong></a></p></td>
<td><p>写入项属性的属性名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549374" data-raw-source="[&lt;strong&gt;wiasSetPropChanged&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549374)"><strong>wiasSetPropChanged</strong></a></p></td>
<td><p>修改属性上下文，以指示更改属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549381" data-raw-source="[&lt;strong&gt;wiasSetPropertyAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549381)"><strong>wiasSetPropertyAttributes</strong></a></p></td>
<td><p>设置访问标志和项的属性的属性值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549390" data-raw-source="[&lt;strong&gt;wiasSetValidFlag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549390)"><strong>wiasSetValidFlag</strong></a></p></td>
<td><p>设置 WIA_PROP_FLAG 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549399" data-raw-source="[&lt;strong&gt;wiasSetValidListFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549399)"><strong>wiasSetValidListFloat</strong></a></p></td>
<td><p>设置类型子 VT_R4 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549409" data-raw-source="[&lt;strong&gt;wiasSetValidListGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549409)"><strong>wiasSetValidListGuid</strong></a></p></td>
<td><p>设置的子类型 VT_CLSID WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549414" data-raw-source="[&lt;strong&gt;wiasSetValidListLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549414)"><strong>wiasSetValidListLong</strong></a></p></td>
<td><p>设置类型子 VT_I4 WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549421" data-raw-source="[&lt;strong&gt;wiasSetValidListStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549421)"><strong>wiasSetValidListStr</strong></a></p></td>
<td><p>设置类型子 VT_BSTR WIA_PROP_LIST 属性的有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549425" data-raw-source="[&lt;strong&gt;wiasSetValidRangeFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549425)"><strong>wiasSetValidRangeFloat</strong></a></p></td>
<td><p>指定子类型 VT_R4 WIA_PROP_RANGE 属性的有效值的范围。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549434" data-raw-source="[&lt;strong&gt;wiasSetValidRangeLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549434)"><strong>wiasSetValidRangeLong</strong></a></p></td>
<td><p>指定子类型 VT_I4 WIA_PROP_RANGE 属性的有效值的范围。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549448" data-raw-source="[&lt;strong&gt;wiasUpdateValidFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549448)"><strong>wiasUpdateValidFormat</strong></a></p></td>
<td><p>为当前的微型驱动程序更新属性上下文的有效格式。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549454" data-raw-source="[&lt;strong&gt;wiasValidateItemProperties&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549454)"><strong>wiasValidateItemProperties</strong></a></p></td>
<td><p>验证针对其当前有效的值的简单项属性的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549475" data-raw-source="[&lt;strong&gt;wiasWriteMultiple&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549475)"><strong>wiasWriteMultiple</strong></a></p></td>
<td><p>将多个属性值写入到 WIA 项 （不同类型的可能是属性）。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549500" data-raw-source="[&lt;strong&gt;wiasWritePropBin&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549500)"><strong>wiasWritePropBin</strong></a></p></td>
<td><p>将一个单一的二进制属性值写入到 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549507" data-raw-source="[&lt;strong&gt;wiasWritePropFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549507)"><strong>wiasWritePropFloat</strong></a></p></td>
<td><p>将浮点属性值写入到 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549512" data-raw-source="[&lt;strong&gt;wiasWritePropGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549512)"><strong>wiasWritePropGuid</strong></a></p></td>
<td><p>将 GUID 属性值写入到 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549515" data-raw-source="[&lt;strong&gt;wiasWritePropLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549515)"><strong>wiasWritePropLong</strong></a></p></td>
<td><p>将长整数属性值写入到 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549525" data-raw-source="[&lt;strong&gt;wiasWritePropStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549525)"><strong>wiasWritePropStr</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549185" data-raw-source="[&lt;strong&gt;wiasDownSampleBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549185)"><strong>wiasDownSampleBuffer</strong></a></p></td>
<td><p>将像素数据和缩减像素采样的缓冲区中指定的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549249" data-raw-source="[&lt;strong&gt;wiasGetImageInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549249)"><strong>wiasGetImageInformation</strong></a></p></td>
<td><p>检索从一个项中传输上下文信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549282" data-raw-source="[&lt;strong&gt;wiasParseEndorserString&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549282)"><strong>wiasParseEndorserString</strong></a></p></td>
<td><p>分析印记签署器字符串，WIA 服务定义和供应商定义字符串中的标记替换为与令牌相关联的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549351" data-raw-source="[&lt;strong&gt;wiasSendEndOfPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549351)"><strong>wiasSendEndOfPage</strong></a></p></td>
<td><p>在数据传输，发送的当前总页计数的过程调用的客户端回调例程。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549441" data-raw-source="[&lt;strong&gt;wiasUpdateScanRect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549441)"><strong>wiasUpdateScanRect</strong></a></p></td>
<td><p>更新扫描设备的扫描区域大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549473" data-raw-source="[&lt;strong&gt;wiasWriteBufToFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549473)"><strong>wiasWriteBufToFile</strong></a></p></td>
<td><p>将临时页缓冲区的内容写入到图像文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549484" data-raw-source="[&lt;strong&gt;wiasWritePageBufToFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549484)"><strong>wiasWritePageBufToFile</strong></a></p></td>
<td><p>将临时页缓冲区的内容写入到图像文件。 使用此函数将页面写入多页 TIFF 文件。</p></td>
</tr>
</tbody>
</table>

 

 

 




