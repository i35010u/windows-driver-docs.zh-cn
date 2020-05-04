---
title: INF UpdateInis 指令
description: UpdateInis 指令指定 INI 文件，从该文件中读取要应用于目标计算机上同名的现有 INI 文件的部分。
ms.assetid: c4717b6c-dc2d-45ba-8b39-3fc33e49466e
keywords:
- INF UpdateInis 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF UpdateInis Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e7cda0992c275158fea20bd3a0394e15375a23c
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223089"
---
# <a name="inf-updateinis-directive"></a>INF UpdateInis 指令


**注意：**  如果要生成通用或移动驱动程序包，则此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**UpdateInis**指令将引用一个或多个命名部分，指定一个 INI 文件，从该文件读取特定的节或行，并将其应用于目标计算机上同名的现有 INI 文件。 此外，还可以在 "*更新-ini" 部分*中指定从和到此类 INI 文件的逐行修改。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
UpdateInis=update-ini-section[,update-ini-section]...
```

由于缺少 INI 文件所必需的，因此在 INF 文件中几乎不会在 Windows 上指定此指令。 但是， **UpdateInis**指令在正式语法语句中所示的任何节中有效，在**AddInterface**指令引用的 INF 编写器定义的部分中有效，或在**InterfaceInstall32**节中引用。

**UpdateInis**指令引用的每个命名部分都具有以下形式：

```inf
[update-ini-section]
 
ini-file,ini-section[,old-ini-entry][,new-ini-entry][,flags]
...
```

*更新-ini 部分*可以有任何由 INF 编写器决定的条目数，每个条目在单独的行中。

## <a name="entries"></a>条目


<a href="" id="ini-file"></a>*ini-文件*  
指定在源媒体上提供的 INI 文件的名称，并隐式指定要在目标计算机上更新的 INI 文件的名称。 此值可以表示为*文件名*，也可以表示为在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。

<a href="" id="ini-section"></a>*ini-部分*  
指定给定 INI 文件中节的名称。 如果指定了接下来的两个值，则此部分包含要更改的项。 如果省略了*旧 ini 条目*，但提供了一个*新的 ini 条目*，则会在读取此部分时添加新条目。

<a href="" id="old-ini-entry"></a>*旧-ini 条目*  
此可选值指定位于给定*ini 节*中的条目的名称，通常用以下格式表示：

```inf
"key=value"
```

*键*和*值*都可以表示为在 INF 文件的**字符串**部分中定义的%*strkey*% 令牌。 星号（**\\**<em>）可指定为 * 键</em>或*值*的通配符。

<a href="" id="new-ini-entry"></a>*新-ini-条目*  
此可选值指定对给定的*旧 ini 项*或添加新项的更改。 此值可以用与*旧 ini 条目*相同的方式表示。

<a href="" id="flags"></a>*随意*  
此可选值控制给定的*旧 ini 条目*和/或*新 ini 条目*的解释。 *标志*条目可以是以下数值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>0</strong></td>
<td align="left"><p>如果省略<em>标志</em>条目，则此值为默认值。</p>
<p>如果 INI 文件中存在给定的<em>旧 ini 输入</em>密钥，请将该<em>key = value</em>替换为给定的新-ini 条目。 只有 INI 文件中的密钥必须匹配。 将忽略每个此类键的对应值。</p>
<p>若要无条件地向目标 INI 文件添加一个<em>新的 ini 条目</em>，请从 INF 的 "<em>更新-ini</em> " 部分的条目中省略 "<em>旧 ini 输入</em>" 值。</p>
<p>若要无条件删除目标 INI 文件中的旧 ini 条目，请忽略新的<em>ini 条目</em>值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>1</strong></td>
<td align="left"><p>如果 INI 文件中存在给定的<em>旧 ini 条目</em>（<em>key = value</em>），请将其替换为具有给定的<em>新 ini 条目</em>的目标 ini 文件。 指定的<em>旧 ini 条目</em>的密钥和值必须与 ini 文件中的<em>密钥</em>和<em>值</em>匹配，以便进行此类替换，而不仅仅是其密钥，因为上述<em>标志</em>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>2</strong></td>
<td align="left"><p>如果在目标 INI 文件中找不到为<em>旧 ini 条目</em>指定的<em>密钥</em>，则不执行任何操作。 否则，所做的更改取决于在 INI 文件中找到的用于<em>旧 ini 条目</em>和<em>新 ini 条目</em>的密钥的匹配项，如下所示：</p>
<ol>
<li><p>如果 INI 文件中存在<em>旧 ini 条目</em>的<em>密钥</em>，但该密钥是<em>新 ini 条目</em>的<em>密钥</em>，请将旧的 ini 条目替换为目标 ini 文件中的<em>新-ini 条目</em>，然后从该 ini 文件中删除多余的 "<em>新 ini" 条目</em>。</p></li>
<li><p>如果 INI 文件中存在<em>旧 ini 条目</em>的<em>密钥</em>，但<em>新 ini 条目</em>的密钥不存在，请将<em>旧</em>ini 输入  <em>密钥</em>替换为目标 ini 文件中的<em>新 ini</em>条目的密钥，但保留<em>旧 ini 条目</em>的值不变。</p></li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><strong>3</strong></td>
<td align="left"><p>如果在 INI 文件中找不到为<em>旧 ini 条目</em>指定的<em>密钥</em>和<em>值</em>，则不执行任何操作。 否则，所做的更改将取决于在 INI 文件中找到的给定<em>键</em>和<em>值</em>的<em>匹配项，</em>如下所示<em>new-ini-entry</em>：</p>
<ol>
<li><p>如果 INI 文件中存在<em>旧 ini 条目</em>的<em>key = 值</em>，但其<em>key = 值</em>为<em>新 ini 条目</em>，请将<em>旧的 ini 条目</em>替换为目标 ini 文件中的<em>新-ini 条目</em>，然后从该 ini 文件中删除多余的<em>新 ini 条目</em>。</p></li>
<li><p>如果 INI 文件中存在<em>旧 ini 条目</em>的<em>key = 值</em>，但<em>新的-ini 条目</em>不存在，请将<em>旧 ini</em>条目替换为目标 ini 文件中的<em>新-ini 条目</em>，但保留<em>旧 ini 条目</em>的值不变。</p></li>
</ol></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

给定的*更新-ini 节*名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

INF 通过以下方式之一在分发介质上提供给定*ini 文件*的完整路径：

-   在 IHV/OEM 提供的 INF 文件中，通过使用此 INF 的 " [**SourceDisksNames**](inf-sourcedisksnames-section.md) " 和 " [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) " 部分显式指定每个命名的源文件的完整路径，该文件不在分发媒体的根目录中。
-   在系统提供的 INF 文件中，通过提供一个或多个其他 INF 文件，在 INF 文件的[**版本**](inf-version-section.md)部分的**LayoutFile**项中标识。

在*旧 ini 条目*或*新 ini 条目*中指定的任何*文件名*都应指定包含该文件的目标目录。 必须将*更新-ini 节*条目中的*文件名*的目标目录路径指定为*dirid*。 有关可能的*dirid*值的列表，请参阅[使用 Dirids](using-dirids.md)。

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**ProfileItems**](inf-profileitems-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**字符串**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**版本**](inf-version-section.md)

 

 






