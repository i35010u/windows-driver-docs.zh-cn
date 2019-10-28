---
title: WIA 实用程序类
ms.assetid: cc20a088-6470-4648-b7d9-999dbd74baf1
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feacee820d973a043176b1a3f4749a89aeed471c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840663"
---
# <a name="wia-utility-classes"></a>WIA 实用程序类


本主题介绍了属于 WIA 实用工具库的三个帮助器类：

-   [CWiauDbgFn 类](#cwiaudbgfn-class)
-   [CWiauFormatConverter 类](#cwiauformatconverter-class)
-   [CWiauPropertyList 类](#cwiaupropertylist-class)

## <a name="cwiaudbgfn-class"></a>CWiauDbgFn 类


[CWiauDbgFn 类](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540345(v=vs.85))是用于函数或方法入口/出口点跟踪的帮助器类。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn)"><strong>CWiauDbgFn::CWiauDbgFn</strong></a></p></td>
<td><p>类构造函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::~CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn)"><strong>CWiauDbgFn：： ~ CWiauDbgFn</strong></a></p></td>
<td><p>类析构函数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiauformatconverter-class"></a>CWiauFormatConverter 类


[CWiauFormatConverter 类](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540363(v=vs.85))是用于将图像转换为 BMP 格式的帮助器类。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter)"><strong>CWiauFormatConverter::CWiauFormatConverter</strong></a></p></td>
<td><p>类构造函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::~CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter)"><strong>CWiauFormatConverter：： ~ CWiauFormatConverter</strong></a></p></td>
<td><p>类析构函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-converttobmp" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::ConvertToBmp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-converttobmp)"><strong>CWiauFormatConverter::ConvertToBmp</strong></a></p></td>
<td><p>将图像转换为 BMP 格式。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-init" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-init)"><strong>CWiauFormatConverter：： Init</strong></a></p></td>
<td><p>初始化用于转换图像的类和 GDI +。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::IsFormatSupported&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported)"><strong>CWiauFormatConverter::IsFormatSupported</strong></a></p></td>
<td><p>验证 GDI + 是否支持要转换的图像格式。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiaupropertylist-class"></a>CWiauPropertyList 类


[CWiauPropertyList 类](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540386(v=vs.85))是用于定义和初始化 WIA 属性列表的帮助器类。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist)"><strong>CWiauPropertyList::CWiauPropertyList</strong></a></p></td>
<td><p>类构造函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::~CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist)"><strong>CWiauPropertyList：： ~ CWiauPropertyList</strong></a></p></td>
<td><p>类析构函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-defineproperty" data-raw-source="[&lt;strong&gt;CWiauPropertyList::DefineProperty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-defineproperty)"><strong>CWiauPropertyList：:D efineProperty</strong></a></p></td>
<td><p>将属性定义添加到属性列表对象。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-getpropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::GetPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-getpropid)"><strong>CWiauPropertyList::GetPropId</strong></a></p></td>
<td><p>获取指定索引处的属性的属性标识符（ID）。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-init" data-raw-source="[&lt;strong&gt;CWiauPropertyList::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-init)"><strong>CWiauPropertyList：： Init</strong></a></p></td>
<td><p>初始化属性列表对象。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::LookupPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid)"><strong>CWiauPropertyList::LookupPropId</strong></a></p></td>
<td><p>获取具有指定属性 ID 的属性的属性索引。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-sendtowia" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SendToWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-sendtowia)"><strong>CWiauPropertyList::SendToWia</strong></a></p></td>
<td><p>调用 WIA 服务来定义属性列表对象中当前包含的所有属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetAccessSubType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong))"><strong>CWiauPropertyList::SetAccessSubType</strong></a></p></td>
<td><p>重置属性的访问权限和子类型。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BYTE*)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85))"><strong>CWiauPropertyList：： System.windows.dependencyobject.setcurrentvalue （BYTE *）</strong></a></p></td>
<td><p>设置其类型为<strong>字节</strong>数组的属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BSTR)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85))"><strong>CWiauPropertyList：： System.windows.dependencyobject.setcurrentvalue （BSTR）</strong></a></p></td>
<td><p>设置类型为<strong>BSTR</strong>的属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(CLSID)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85))"><strong>CWiauPropertyList：： System.windows.dependencyobject.setcurrentvalue （CLSID）</strong></a></p></td>
<td><p>设置其类型为<strong>CLSID</strong>的属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(FLOAT)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85))"><strong>CWiauPropertyList：： System.windows.dependencyobject.setcurrentvalue （FLOAT）</strong></a></p></td>
<td><p>设置类型为<strong>FLOAT</strong>的属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(LONG)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85))"><strong>CWiauPropertyList：： System.windows.dependencyobject.setcurrentvalue （LONG）</strong></a></p></td>
<td><p>设置类型为<strong>LONG</strong>的属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(SYSTEMTIME)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85))"><strong>CWiauPropertyList：： System.windows.dependencyobject.setcurrentvalue （SYSTEMTIME）</strong></a></p></td>
<td><p>设置属性的值，该属性的类型为<strong>SYSTEMTIME</strong> （如 Microsoft Windows SDK 文档中所述）。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(BSTR, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （BSTR，list）</strong></a></p></td>
<td><p>设置类型，以及<strong>BSTR</strong>值列表的默认值、当前值和有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(CLSID, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （CLSID，list）</strong></a></p></td>
<td><p>设置类型，以及<strong>CLSID</strong>值列表的默认值、当前值和有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(flag)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （标志）</strong></a></p></td>
<td><p>设置类型以及属性的默认值、当前值和有效值，它们的值由标记设置确定。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （FLOAT，list）</strong></a></p></td>
<td><p>设置类型，以及<strong>浮点</strong>值列表的默认值、当前值和有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （FLOAT，range）</strong></a></p></td>
<td><p>设置类型，以及<strong>浮点</strong>值范围的默认值、当前值和有效值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （LONG，list）</strong></a></p></td>
<td><p>设置类型，以及<strong>长</strong>值列表的默认值、当前值和有效值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85))"><strong>CWiauPropertyList：： SetValidValues （LONG，range）</strong></a></p></td>
<td><p>设置类型，以及<strong>LONG</strong>值范围的默认值、当前值和有效值。</p></td>
</tr>
</tbody>
</table>

 

 

 




