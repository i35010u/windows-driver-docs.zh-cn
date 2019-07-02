---
title: DevCon FindAll
description: 查找计算机，包括一次连接到计算机，但已分离或移动设备上的所有设备。
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
ms.openlocfilehash: 3a2deff3d2e6c91cc2b846c39643c9bd4c44c083
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492506"
---
# <a name="devcon-findall"></a>DevCon FindAll


查找计算机，包括一次连接到计算机，但已分离或移动设备上的所有设备。 (这些参数称为虚幻设备或*幻像*设备。)**DevCon FindAll**操作还会找到设备，它们以不同方式枚举结果的 BIOS 更改。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] findall {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconfindalltoolsspanspan-idddkdevconfindalltoolsspanparameters"></a><span id="ddk_devcon_findall_tools"></span><span id="DDK_DEVCON_FINDALL_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和更高版本的 Windows 的计算机上，组策略默认情况下禁用远程访问服务。



<span id="______________"></span> **\\** *   
表示在计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定全部或部分硬件 ID、 兼容 ID 或设备的设备实例 ID。 在指定多个 Id 时，键入一个空格之间每个 id。 包含一个 & 字符的 Id ( **&** ) 必须括在引号中。

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
<td align="left"><p>匹配任何字符或任何字符。 使用通配符字符 (</em>) 创建 ID 模式，例如，<em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>例如，指示设备实例 ID <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义的字符串匹配 （严格按其显示）。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>'*PNP0600</strong>，其中 *PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>  



<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>类</em>指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**findall**)。 否则，将忽略 DevCon **/m**参数并在其中搜索本地计算机而不返回语法错误。

若要查找当前连接到计算机的设备，请使用[ **DevCon 查找**](devcon-find.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon resources STORAGE\Volume
devcon resources =ports lpt*
devcon resources @pci*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例 22:查找 （并查找所有） 安装程序类中的设备](devcon-examples.md#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)









