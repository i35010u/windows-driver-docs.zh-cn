---
title: DevCon FindAll
description: 查找计算机上的所有设备，包括已连接到计算机但已分离或移动的设备。
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
ms.openlocfilehash: d97b67615cf406afc8ca99ff80a24e8df250048a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783393"
---
# <a name="devcon-findall"></a>DevCon FindAll

查找计算机上的所有设备，包括已连接到计算机但已分离或移动的设备。  (这些称为 "nonpresent 设备" 或 " *虚拟* 设备"。 ) **DevCon FindAll** 操作还会发现因 BIOS 更改而枚举为不同的设备。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] findall {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_findall_toolsspanspan-idddk_devcon_findall_toolsspanparameters"></a><span id="ddk_devcon_findall_tools"></span><span id="DDK_DEVCON_FINDALL_TOOLS"></span>参数

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span>**/m： \\ \\**<em>计算机</em>在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**   若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和更高版本的 Windows 的计算机上，默认情况下组策略禁用对服务的远程访问。

<span id="______________"></span> **\** _ 表示计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> _ID * 指定设备的硬件 ID、兼容 ID 或设备实例 ID 的全部或部分。 指定多个 Id 时，请在每个 ID 之间键入一个空格。 包含与号字符 () 的 Id **&** 必须用引号引起来。

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
<td align="left"><p>匹配任何字符或不匹配任何字符。 使用通配符 (</em>) 创建 ID 模式，例如 <em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>指示设备实例 ID，例如 <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p> (单引号) </p></td>
<td align="left"><p>按原义 (与) 显示的内容完全匹配。 在字符串前面加上单引号，指示星号是 ID 名称的一部分，并且不是通配符，例如 <strong>"* PNP0600</strong>，其中，* PNP0600 (包括星号) 为硬件 ID。</p></td>
</tr>
</tbody>
</table>  

<span id="________class______"></span><span id="________CLASS______"></span>**=**<em>类</em>指定设备的设备安装程序类。 等号 (**=**) 将字符串标识为类名。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M** 参数必须位于操作名称的前面 (**findall**) 。 否则，DevCon 将忽略 **/m** 参数，并在本地计算机上搜索，而不返回语法错误。

若要仅查找当前连接到计算机的设备，请使用 [**DevCon find**](devcon-find.md) 操作。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon resources STORAGE\Volume
devcon resources =ports lpt*
devcon resources @pci*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例22：查找 (并查找安装类中的所有) 设备](devcon-examples.md#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)
