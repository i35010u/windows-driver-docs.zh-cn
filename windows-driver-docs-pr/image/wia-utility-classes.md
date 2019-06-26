---
title: WIA 实用程序类
ms.assetid: cc20a088-6470-4648-b7d9-999dbd74baf1
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe433e5f5a2d40a1379dd2b0b110491c40b49371
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387338"
---
# <a name="wia-utility-classes"></a>WIA 实用程序类


本主题介绍 WIA 实用工具库一部分的三个帮助程序类：

-   [CWiauDbgFn 类](#cwiaudbgfn-class)
-   [CWiauFormatConverter 类](#cwiauformatconverter-class)
-   [CWiauPropertyList 类](#cwiaupropertylist-class)

## <a name="cwiaudbgfn-class"></a>CWiauDbgFn 类


[CWiauDbgFn 类](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540345(v=vs.85))是一个帮助器类的函数或方法的入口/出口点跟踪。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn)"><strong>CWiauDbgFn::CWiauDbgFn</strong></a></p></td>
<td><p>类构造函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::~CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn)"><strong>CWiauDbgFn::~CWiauDbgFn</strong></a></p></td>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter)"><strong>CWiauFormatConverter::CWiauFormatConverter</strong></a></p></td>
<td><p>类构造函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::~CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter)"><strong>CWiauFormatConverter::~CWiauFormatConverter</strong></a></p></td>
<td><p>类析构函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-converttobmp" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::ConvertToBmp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-converttobmp)"><strong>CWiauFormatConverter::ConvertToBmp</strong></a></p></td>
<td><p>将图像转换为 BMP 格式。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-init" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-init)"><strong>CWiauFormatConverter::Init</strong></a></p></td>
<td><p>转换图像初始化类和 GDI +。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::IsFormatSupported&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported)"><strong>CWiauFormatConverter::IsFormatSupported</strong></a></p></td>
<td><p>验证在 GDI + 支持要转换的映像格式。</p></td>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist)"><strong>CWiauPropertyList::CWiauPropertyList</strong></a></p></td>
<td><p>类构造函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::~CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist)"><strong>CWiauPropertyList:: ~ CWiauPropertyList</strong></a></p></td>
<td><p>类析构函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-defineproperty" data-raw-source="[&lt;strong&gt;CWiauPropertyList::DefineProperty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-defineproperty)"><strong>CWiauPropertyList::DefineProperty</strong></a></p></td>
<td><p>将属性定义添加到属性列表对象。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-getpropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::GetPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-getpropid)"><strong>CWiauPropertyList::GetPropId</strong></a></p></td>
<td><p>获取指定索引处的属性的属性标识符 (ID)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-init" data-raw-source="[&lt;strong&gt;CWiauPropertyList::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-init)"><strong>CWiauPropertyList::Init</strong></a></p></td>
<td><p>初始化的属性列表对象。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::LookupPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid)"><strong>CWiauPropertyList::LookupPropId</strong></a></p></td>
<td><p>获取与指定的属性 ID 的属性的属性索引</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-sendtowia" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SendToWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-sendtowia)"><strong>CWiauPropertyList::SendToWia</strong></a></p></td>
<td><p>调用 WIA 服务，以定义当前属性列表对象中包含的所有属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetAccessSubType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong))"><strong>CWiauPropertyList::SetAccessSubType</strong></a></p></td>
<td><p>重置的访问权限和属性的子类型。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BYTE*)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(BYTE*)</strong></a></p></td>
<td><p>设置类型为的属性的值<strong>字节</strong>数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BSTR)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(BSTR)</strong></a></p></td>
<td><p>设置为其类型的属性的值<strong>BSTR</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(CLSID)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(CLSID)</strong></a></p></td>
<td><p>设置为其类型的属性的值<strong>CLSID</strong>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(FLOAT)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(FLOAT)</strong></a></p></td>
<td><p>设置为其类型的属性的值<strong>FLOAT</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(LONG)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(LONG)</strong></a></p></td>
<td><p>设置为其类型的属性的值<strong>长</strong>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(SYSTEMTIME)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(SYSTEMTIME)</strong></a></p></td>
<td><p>设置为其类型的属性的值<strong>SYSTEMTIME</strong> （Microsoft Windows SDK 文档中所述）。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(BSTR, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85))"><strong>CWiauPropertyList::SetValidValues （BSTR，列表）</strong></a></p></td>
<td><p>设置类型，以及默认情况下，最新的且有效的值的一系列<strong>BSTR</strong>值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(CLSID, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85))"><strong>CWiauPropertyList::SetValidValues （CLSID，列表）</strong></a></p></td>
<td><p>设置类型，以及默认情况下，最新的且有效的值的一系列<strong>CLSID</strong>值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(flag)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85))"><strong>CWiauPropertyList::SetValidValues(flag)</strong></a></p></td>
<td><p>设置类型，以及默认情况下，其值均由标志设置的属性的最新的且有效的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85))"><strong>CWiauPropertyList::SetValidValues(FLOAT, list)</strong></a></p></td>
<td><p>设置类型，以及默认情况下，最新的且有效的值的一系列<strong>FLOAT</strong>值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85))"><strong>CWiauPropertyList::SetValidValues(FLOAT, range)</strong></a></p></td>
<td><p>设置类型，以及默认情况下，最新的且有效的值的一系列<strong>FLOAT</strong>值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85))"><strong>CWiauPropertyList::SetValidValues （LONG，列表）</strong></a></p></td>
<td><p>设置类型，以及默认情况下，最新的且有效的值的一系列<strong>长</strong>值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85))"><strong>CWiauPropertyList::SetValidValues （长型值，范围）</strong></a></p></td>
<td><p>设置类型，以及默认情况下，最新的且有效的值的一系列<strong>长</strong>值。</p></td>
</tr>
</tbody>
</table>

 

 

 




