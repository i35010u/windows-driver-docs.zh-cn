---
title: 使用 GetGlobalAttribute
description: 使用 GetGlobalAttribute
ms.assetid: 0e23ecba-7d89-44f5-b6a7-7d6be9a56765
keywords:
- GetGlobalAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 293b09cc5cd8bbcd0a958b046fa10fb5649956ec
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209241"
---
# <a name="using-getglobalattribute"></a>使用 GetGlobalAttribute





所有全局属性名称都与 *PostScript 打印机说明文件格式规范（v4.0）* 中定义的关键字名称相同。 有关其语义，请参阅此规范。  (此资源可能在某些语言和国家/地区不可用。 ) 

在下表中， *pdwDataType* 参数采用 [**EATTRIBUTE \_ DATATYPE**](/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype) 枚举类型的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>全局特性</th>
<th>输出参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CenterRegistered</strong></p></td>
<td><p><em>pdwDataType： kADT_BOOL</p>
<p><em></em>pbData </em> ： <strong>TRUE</strong> 或 <strong>FALSE</strong></p>
<p><em><em>pcbNeeded</em>： <strong>sizeof</strong> (BOOL) </p></td>
</tr>
<tr class="even">
<td><p><strong>ColorDevice</strong></p></td>
<td><p></em>pdwDataType： kADT_BOOL</p>
<p><em><em>pbData</em>： <strong>TRUE</strong> 或 <strong>FALSE</strong></p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (BOOL) </p></td>
</tr>
<tr class="odd">
<td><p><strong>扩展</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>： ASCII 字符串 (MULTI_SZ 格式，) 包含打印机支持的 extensionOption 的注册值。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包括最后一个空字符) </p>
<p>注意： " <em> filesystem： True" 被视为具有 "filesystem" 选项的<strong> </em> 扩展</strong>。 "FileSystem： False" 被视为 <em> 不具有 "filesystem" 选项的扩展。</p></td>
</tr>
<tr class="even">
<td><p><strong>FileVersion</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_DWORD</p>
<p><em><em>pbData</em>：一个 DWORD 值，其高序位字包含主要版本号，其低序位字包含次版本号。</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (DWORD) </p></td>
</tr>
<tr class="odd">
<td><p><strong>FreeVM</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_DWORD</p>
<p><em></em>pbData </em> ： FreeVM 的值 <em></p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (DWORD) </p></td>
</tr>
<tr class="even">
<td><p><strong>LandscapeOrientation</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>： "Plus90" 或 "Minus90" 的以 NULL 结尾的 ASCII 字符串。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包括最后一个空字符) </p>
<p>注意：仅当 PPD 包含 " <em> LandscapeOrientation： Minus90" 时返回 "Minus90"。 在所有其他情况下，将返回 "Plus90"。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LanguageEncoding</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_ASCII</p>
<p><em>pbData</em>：以 NULL 结尾的 ASCII 字符串，其中包含以下 encodingOption 值之一：</p>
<p>"ISOLatin1"</p>
<p>Unicode</p>
<p>"JIS83-RKSJ"</p>
<p>"None"</p>
<p><em><em>pcbNeeded</em>： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包括最后一个空字符) </p>
<p>说明</p>
<p>"WindowsANSI" 与 "ISOLatin1" 的处理方式相同。 不支持其他 encodingOption 值。</p>
<p>如果不存在 * LanguageEncoding，则使用 * LanguageVersion 来推导返回值。</p></td>
</tr>
<tr class="even">
<td><p><strong>LanguageLevel</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_DWORD</p>
<p><em><em>pbData</em>：打印机支持的 PostScript 语言级别</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (DWORD) </p></td>
</tr>
<tr class="odd">
<td><p><strong>昵称</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_UNICODE</p>
<p><em>pbData</em>：如果存在 * ShortNickName，则为以 NULL 结尾的 PPD * ShortNickName 值的 Unicode 字符串; 如果缺少 * ShortNickName，则为 * 别名值。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 Unicode 字符串的字节计数 (包括最后一个空字符) </p></td>
</tr>
<tr class="even">
<td><p><strong>PPD-Adobe</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_DWORD</p>
<p><em></em>pbData </em> ：一个 DWORD 值，其高序位字包含主要版本号，其低序位字包含次版本号。</p>
<p><em><em>pcbNeeded</em>： <strong>sizeof</strong> (DWORD) </p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintPSErrors</strong></p></td>
<td><p></em>pdwDataType： kADT_BOOL</p>
<p><em><em>pbData</em>： <strong>TRUE</strong> 或 <strong>FALSE</strong></p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (BOOL) </p>
<p>注意：如果 <em> PrintPSErrors 不存在，则假定为 <strong>TRUE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Product</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_BINARY</p>
<p><em>pbData</em>： <em> 产品值</p>
<p><em></em>pcbNeeded </em> ：输出二进制数据的字节计数</p>
<p>注意：仅返回第一个 <em> 产品条目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>协议</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_ASCII</p>
<p><em>pbData</em>： ASCII 字符串 (MULTI_SZ 格式，) 包含打印机支持的 protocolOption 的注册值。</p>
<p><em><em>pcbNeeded</em>： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包括最后一个空字符) </p></td>
</tr>
<tr class="even">
<td><p><strong>PSVersion</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_BINARY</p>
<p><em>pbData</em>： <em> PSVersion 值</p>
<p><em></em>pcbNeeded </em> ：输出二进制数据的字节计数</p>
<p>注意：仅返回第一个 <em> PSVersion 条目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SuggestedJobTimeout</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_DWORD</p>
<p><em><em>pbData</em>： * SuggestedJobTimeout 值。 如果从 PPD 中没有它，则默认情况下返回0。</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (DWORD) </p></td>
</tr>
<tr class="even">
<td><p><strong>SuggestedWaitTimeout</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_DWORD</p>
<p><em></em>pbData </em> ： <em> SuggestedWaitTimeout 值。 如果它不存在于 PPD 中，则默认情况下将返回300。</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (DWORD) </p></td>
</tr>
<tr class="odd">
<td><p><strong>吞吐量</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_DWORD</p>
<p><em></em>pbData </em> ： <em> 吞吐量值。 如果它不存在于 PPD 中，则默认情况下返回0。</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (DWORD) </p></td>
</tr>
<tr class="even">
<td><p><strong>TTRasterizer</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：以 NULL 结尾的 ASCII 字符串，其中包含以下 rasterizerOption 值之一：</p>
<p>"None"</p>
<p>"Accept68K"</p>
<p>"Type42"</p>
<p>"TrueImage"</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包括最后一个空字符) </p>
<p>注意：如果缺少 * TTRasterizer 条目，则返回 "None"。</p></td>
</tr>
</tbody>
</table>

 

 

