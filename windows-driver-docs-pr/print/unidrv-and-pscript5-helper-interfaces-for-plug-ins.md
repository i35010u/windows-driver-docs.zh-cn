---
title: 插件的 Unidrv 和 Pscript5 帮助程序接口
description: 插件的 Unidrv 和 Pscript5 帮助程序接口
ms.assetid: 043a38f7-200c-4f1d-b937-4ddd6e2045dd
keywords:
- IPrintCoreHelperPS
- IPrintCoreHelperUni
- IPrintCoreHelper
- helper 接口 WDK 打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b97a74a881c70048f70c9258da209475e61d2a7c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213085"
---
# <a name="unidrv-and-pscript5-helper-interfaces-for-plug-ins"></a>插件的 Unidrv 和 Pscript5 帮助程序接口


由于 [IPrintCoreHelperPS](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps) 和 [IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni) 接口继承自 [IPrintCoreHelper](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper) 接口，因此所有这三个接口都共享一组公共方法。 下表列出了帮助程序接口中的方法，并说明了哪些方法在所有三个接口中可用，哪些方法仅在一个接口中可用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>包含在</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConvertStringToPTFormat</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>ConvertDefaultGDLSnapshot</strong></p></td>
<td><p>仅限<strong>IPrintCoreHelperUni</strong>接口</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConvertGDLSnapshot</strong></p></td>
<td><p>仅限<strong>IPrintCoreHelperUni</strong>接口</p></td>
</tr>
<tr class="even">
<td><p><strong>CreateInstanceOfMSXMLObject</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumConstrainedOptions</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumFeatures</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumOptions</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>GetFeatureAttribute</strong></p></td>
<td><p>仅限<strong>IPrintCoreHelperPS</strong>接口</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetGlobalAttribute</strong></p></td>
<td><p>仅限<strong>IPrintCoreHelperPS</strong>接口</p></td>
</tr>
<tr class="even">
<td><p><strong>GetOptionAttribute</strong></p></td>
<td><p>仅限<strong>IPrintCoreHelperPS</strong>接口</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetOption</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>SetOptions</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="odd">
<td><p><strong>WhyConstrained</strong></p></td>
<td><p>全部</p></td>
</tr>
</tbody>
</table>

 

 

