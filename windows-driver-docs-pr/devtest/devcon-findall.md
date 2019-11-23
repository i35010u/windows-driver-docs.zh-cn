---
title: DevCon FindAll
description: 查找计算机上的所有设备，包括已连接到计算机但已分离或移动的设备。
ms.assetid: 63148bb4-dc54-4b82-9e8f-d6967ad86d74
keywords:
- DevCon FindAll 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon FindAll
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f0035362447daa94d657b9a5fd107504b7d33e0
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038045"
---
# <a name="devcon-findall"></a>DevCon FindAll

查找计算机上的所有设备，包括已连接到计算机但已分离或移动的设备。 （这些设备称为 nonpresent 设备或*虚拟*设备。）**DevCon FindAll**操作还会发现因 BIOS 更改而进行了不同枚举的设备。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] findall {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_findall_toolsspanspan-idddk_devcon_findall_toolsspanparameters"></a><span id="ddk_devcon_findall_tools"></span><span id="DDK_DEVCON_FINDALL_TOOLS"></span>Parameters

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m：\\\\** <em>计算机</em>在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**  若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和更高版本的 Windows 的计算机上，默认情况下组策略禁用对服务的远程访问。

<span id="______________"></span> **\*** 表示计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span>*ID*指定设备的硬件 id、兼容 ID 或设备实例 id 的全部或部分。 指定多个 Id 时，请在每个 ID 之间键入一个空格。 包含 "&" 符（ **&** ）的 id 必须用引号引起来。

以下特殊字符修改 ID 参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符（</em>）创建 ID 模式，例如<em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>指示设备实例 ID，例如<strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义（与它显示的完全相同）匹配字符串。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>'*PNP0600</strong>，其中 *PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>  

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>类</em>指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M**参数必须位于操作名称（**findall**）之前。 否则，DevCon 将忽略 **/m**参数，并在本地计算机上搜索，而不返回语法错误。

若要仅查找当前连接到计算机的设备，请使用[**DevCon find**](devcon-find.md)操作。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon resources STORAGE\Volume
devcon resources =ports lpt*
devcon resources @pci*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>实例

[示例22：在安装程序类中查找（和查找所有）设备](devcon-examples.md#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)
