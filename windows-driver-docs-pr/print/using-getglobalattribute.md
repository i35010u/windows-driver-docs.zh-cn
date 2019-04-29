---
title: 使用 GetGlobalAttribute
description: 使用 GetGlobalAttribute
ms.assetid: 0e23ecba-7d89-44f5-b6a7-7d6be9a56765
keywords:
- GetGlobalAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72024925395119dc0d54843b09a0d09d88c93b5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373461"
---
# <a name="using-getglobalattribute"></a>使用 GetGlobalAttribute





所有全局特性名称都相同中定义的关键字名称*PostScript 打印机说明文件格式规范、 v4.3*。 请参阅其语义此规范。 （此资源可能不会在某些语言和国家/地区中可用。）

下表中*pdwDataType*参数接受值为[ **EATTRIBUTE\_数据类型**](https://msdn.microsoft.com/library/windows/hardware/ff548692)枚举类型。

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
<td><p><em>pdwDataType: kADT_BOOL</p>
<p>pbData</em>:<strong>TRUE</strong>或<strong>FALSE</strong></p>
<p><em><em>pcbNeeded</em>: <strong>sizeof</strong>(BOOL)</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorDevice</strong></p></td>
<td><p></em>pdwDataType: kADT_BOOL</p>
<p><em><em>pbData</em>:<strong>TRUE</strong>或<strong>FALSE</strong></p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(BOOL)</p></td>
</tr>
<tr class="odd">
<td><p><strong>扩展插件</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:打印机支持的 extensionOption 的 ASCII 字符串 （格式为 MULTI_SZ） 包含已注册的值。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括最后一个 null 字符）</p>
<p>注意："<em>文件系统：True"被视为如同<strong></em>扩展</strong>都有"文件系统"选项。 "文件系统：False"被视为如同<em>扩展不具有"文件系统"选项。</p></td>
</tr>
<tr class="even">
<td><p><strong>FileVersion</strong></p></td>
<td><p>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>pbData</em>： 一个 dword 值，其高序位字包含主版本号，其低序位字包含的次版本号。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>FreeVM</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>： 值<em>FreeVM</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>LandscapeOrientation</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:"Plus90"或"Minus90"的以 NULL 结尾 ASCII 字符串。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括最后一个 null 字符）</p>
<p>注意：仅当 PPD 包含时返回"Minus90""<em>LandscapeOrientation:Minus90"。 在所有其他情况下，返回"Plus90"。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LanguageEncoding</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:以 NULL 结尾包含 ASCII 字符串的以下 encodingOption 值之一：</p>
<p>"ISOLatin1"</p>
<p>"Unicode"</p>
<p>"JIS83-RKSJ"</p>
<p>"None"</p>
<p><em><em>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括最后一个 null 字符）</p>
<p>说明</p>
<p>被视为"WindowsANSI"与"ISOLatin1"相同。 不支持其他 encodingOption 值。</p>
<p>如果 * LanguageEncoding 不存在，* LanguageVersion 用于推导的返回值。</p></td>
</tr>
<tr class="even">
<td><p><strong>LanguageLevel</strong></p></td>
<td><p>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>pbData</em>:PostScript 语言级别支持的打印机</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>NickName</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>pbData</em>:将 Unicode 字符串以 NULL 结尾的 PPD * ShortNickName 值如果 * ShortNickName 是否存在，或 * 别名值，如果 * ShortNickName 不存在。</p>
<p>pcbNeeded</em>： 指向 Unicode 字符串的字节数<em>pbData</em> （包括最后一个 null 字符）</p></td>
</tr>
<tr class="even">
<td><p><strong>PPD-Adobe</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>： 一个 dword 值，其高序位字包含主版本号，其低序位字包含的次版本号。</p>
<p><em><em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintPSErrors</strong></p></td>
<td><p></em>pdwDataType: kADT_BOOL</p>
<p><em><em>pbData</em>:<strong>TRUE</strong>或<strong>FALSE</strong></p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(BOOL)</p>
<p>注意：如果<em>PrintPSErrors 不存在，它被假定为<strong>TRUE</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Product</strong></p></td>
<td><p>pdwDataType</em>: kADT_BINARY</p>
<p><em>pbData</em>:<em>产品值</p>
<p>pcbNeeded</em>： 输出二进制数据的字节数</p>
<p>注意： 只有第一个<em>返回产品条目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>协议</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:打印机支持的 protocolOption 的 ASCII 字符串 （格式为 MULTI_SZ） 包含已注册的值。</p>
<p><em><em>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括最后一个 null 字符）</p></td>
</tr>
<tr class="even">
<td><p><strong>PSVersion</strong></p></td>
<td><p>pdwDataType</em>: kADT_BINARY</p>
<p><em>pbData</em>: <em>PSVersion 值</p>
<p>pcbNeeded</em>： 输出二进制数据的字节数</p>
<p>注意： 只有第一个<em>返回 PSVersion 条目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SuggestedJobTimeout</strong></p></td>
<td><p>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>pbData</em>: * SuggestedJobTimeout 值。 如果它不存在从 PPD，默认情况下返回 0。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>SuggestedWaitTimeout</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>: <em>SuggestedWaitTimeout 值。 如果不存在 PPD 中，默认情况下返回 300。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>吞吐量</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>:<em>吞吐量值。 如果不存在 PPD 中，默认情况下返回 0。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>TTRasterizer</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>： 包含下列 rasterizerOption 值之一的以 NULL 结尾的 ASCII 字符串：</p>
<p>"None"</p>
<p>"Accept68K"</p>
<p>"Type42"</p>
<p>"TrueImage"</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括最后一个 null 字符）</p>
<p>注意： 如果 * TTRasterizer 项不存在，"None"返回。</p></td>
</tr>
</tbody>
</table>

 

 

 




