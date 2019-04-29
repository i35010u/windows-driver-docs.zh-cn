---
title: INF UpdateInis 指令
description: UpdateInis 指令指定从中进行读取的部分应用于目标计算机上的相同名称的现有 INI 文件 INI 文件。
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
ms.openlocfilehash: a67243a4c387317b5d5b60bab28915d27b52221d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363223"
---
# <a name="inf-updateinis-directive"></a>INF UpdateInis 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**UpdateInis**指令引用一个或多个命名的部分，指定的 INI 文件中的特定部分或行即为读取和应用到目标计算机上的相同名称的现有 INI 文件。 （可选） 中指定从 / 向此类 INI 文件的行按行修改*更新 ini 部分*。

```ini
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

INF 文件安装在 Windows 中，由于缺少必备的 INI 文件中几乎不会指定此指令。 但是， **UpdateInis**指令中所示在正式语法语句中，以及引用的 INF 编写器定义部分中的部分是有效**AddInterface**指令或在被引用**InterfaceInstall32**部分。

每个命名部分引用的**UpdateInis**指令具有以下形式：

```ini
[update-ini-section]
 
ini-file,ini-section[,old-ini-entry][,new-ini-entry][,flags]
...
```

*更新 ini 部分*可以具有任意 INF 编写器确定数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="ini-file"></a>*ini-file*  
指定提供的源媒体在和上，隐式地，要在目标计算机上更新的 INI 文件 INI 文件的名称。 此值可以表示为*文件名*或作为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md) INF 文件部分。

<a href="" id="ini-section"></a>*ini-section*  
指定给定的 INI 文件中节的名称。 如果指定了接下来两个值，本部分包含要更改的项。 如果*旧 ini 条目*省略但*新 ini 条目*提供新的条目是要阅读本部分中添加。

<a href="" id="old-ini-entry"></a>*old-ini-entry*  
此可选值指定的名称中的条目的给定*ini 部分*通常表示为以下形式：

```ini
"key=value"
```

一个或两个*键*并*值*可表示为 %*strkey*中定义的 %令牌**字符串**INF 文件部分。 星号 (**\\**<em>) 可以为指定的通配符为 * 键</em>或*值*。

<a href="" id="new-ini-entry"></a>*new-ini-entry*  
此可选值指定为更改给定*旧 ini 条目*或添加新条目。 此值可以以与相同的方式表示*旧 ini 条目*。

<a href="" id="flags"></a>*flags*  
此可选值控制的解释给定*旧 ini 条目*和/或*新 ini 条目*。 *标志*条目可以是以下数值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>0</strong></td>
<td align="left"><p>这是默认值<em>标志</em>如果省略的条目。</p>
<p>如果给定<em>旧 ini 条目</em>INI 文件中存在密钥，、 将其替换<em>键 = 值</em>包含给定新的 ini 的条目。 仅在 INI 文件中的密钥必须匹配。 将忽略每个此类密钥的相应值。</p>
<p>若要添加<em>新 ini 条目</em>无条件地到目标 INI 文件中，省略<em>旧 ini 条目</em>从中的条目的值<em>更新 ini</em> INF 部分。</p>
<p>若要从目标 INI 文件无条件地删除旧 ini 条目，请省略<em>新 ini 条目</em>值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>1</strong></td>
<td align="left"><p>如果给定<em>旧 ini 条目</em>(<em>键 = 值</em>) 存在在 INI 文件中，将为它具有目标 INI 文件中给定<em>新 ini 条目</em>。 这两个<em>键</em>并<em>值</em>指定<em>旧 ini 条目</em>必须匹配此类替换来进行，而不仅仅是其键与上述的INI文件中<em>标志</em>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>2</strong></td>
<td align="left"><p>如果<em>键</em>为指定<em>旧 ini 条目</em>无法找到目标 INI 文件中，不执行任何操作。 否则，在给定的键的 INI 文件中找到的更改取决于匹配<em>旧 ini 条目</em>并<em>新 ini 条目</em>，按如下所示：</p>
<ol>
<li><p>如果<em>键</em>的<em>旧 ini 条目</em>INI 文件中存在，但也越来越高<em>密钥</em>的<em>新 ini 条目</em>，替换旧 ini 条目与<em>新 ini 条目</em>目标 INI 文件，然后，删除多余<em>新 ini 条目</em>从该 INI 文件。</p></li>
<li><p>如果<em>密钥</em>的<em>旧 ini 条目</em>INI 文件，但的键中存在<em>新 ini 条目</em>does not、 替换<em>旧 ini 条目</em>  <em>键</em>与<em>新 ini 条目</em>目标 INI 文件，但保留的值<em>旧 ini 条目</em>不变。</p></li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><strong>3</strong></td>
<td align="left"><p>如果<em>键</em>并<em>值</em>指定为<em>旧 ini 条目</em>不能在 INI 文件中找到，不执行任何操作。 否则，在 INI 文件中找到的更改取决于匹配给定<em>密钥</em>并<em>值</em>的<em>旧 ini 条目</em>和<em>新 ini-输入</em>，按如下所示：</p>
<ol>
<li><p>如果<em>键 = 值</em>的<em>旧 ini 条目</em>INI 文件中存在，但也越来越高<em>键 = 值</em>的<em>新 ini 条目</em>，替换<em>旧 ini 条目</em>与<em>新 ini 条目</em>目标 INI 文件，然后，删除多余<em>新 ini 条目</em>从该 INI 文件。</p></li>
<li><p>如果<em>密钥 = value</em>的<em>旧 ini 条目</em>INI 文件中存在但<em>新 ini 条目</em>does not、 替换<em>旧 ini 条目</em>与<em>新 ini 条目</em>目标 INI 文件，但保留的值<em>旧 ini 条目</em>不变。</p></li>
</ol></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

给定*更新 ini 部分*名称必须是唯一的 INF 文件中的和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

INF 提供的完整路径给定*ini 文件*中通过以下方式之一在分发媒体：

-   在提供 IHV/OEM INF 文件中，通过使用[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)并[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分到此 INF 显式指定在分发媒体的根目录 （或目录） 中不是每个命名的源文件的完整路径。
-   在系统提供 INF 文件中，通过提供一个或多个附加 INF 文件中标识**LayoutFile**中的条目[**版本**](inf-version-section.md) INF 文件部分。

任何*文件名*中指定*旧 ini 条目*或*新 ini 条目*应指定包含该文件的目标目录。 此类的目标目录路径*文件名*中*更新 ini 部分*条目必须指定为*dirid*。 有关可能的列表*dirid*值，请参阅[使用 Dirids](using-dirids.md)。

## <a name="see-also"></a>请参阅


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

[**Strings**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**版本**](inf-version-section.md)

 

 






