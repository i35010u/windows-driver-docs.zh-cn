---
title: DevCon Resources
description: 列出分配给指定设备的资源。 资源是可分配的和可寻址的总线路径，如 DMA 通道、i/o 端口、IRQ 和内存地址。 在本地和远程计算机上有效。
ms.assetid: 06bf2a5a-07a1-42b4-90db-ed74ce84d075
keywords:
- DevCon 资源驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Resources
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23b3e110875149291c06ae52d5f64f0acdafe815
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038040"
---
# <a name="devcon-resources"></a>DevCon Resources

列出分配给指定设备的资源。 资源是可分配的和可寻址的总线路径，如 DMA 通道、i/o 端口、IRQ 和内存地址。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] resources {* | ID [ID ...] | =class [ID [ID...]]}
```

## <a name="span-idddk_devcon_resources_toolsspanspan-idddk_devcon_resources_toolsspanparameters"></a><span id="ddk_devcon_resources_tools"></span><span id="DDK_DEVCON_RESOURCES_TOOLS"></span>Parameters

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m： \\ @ no__t**<em>计算机</em>在指定的远程计算机上运行命令。 反斜杠是必需的。

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
<td align="left"><p>按原义（与它显示的完全相同）匹配字符串。 在字符串前面加上单引号，指示星号是 ID 名称的一部分，并且不是通配符，如<strong>"* PNP0600"</strong>，其中 * PNP0600 （包括星号）是硬件 ID。</p></td>
</tr>
</tbody>
</table>  

<span id="________class______"></span><span id="________CLASS______"></span> **@no__t 3**<em>类</em>指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

你还可以在类名称后指定硬件 Id、兼容 Id、设备实例 Id 或 ID 模式。 键入每个 ID 或模式之间的空格。 DevCon 在类中查找与指定 Id 相匹配的设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M**参数必须位于操作名称（**资源**）之前。 否则，DevCon 将忽略 **/m**参数，并显示分配给本地计算机上的设备的资源，而不会返回语法错误。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon resources *
devcon /m:\\server01 resources =media
devcon resources acpi* *port*
devcon resources =class port* (by class and hardware ID)
devcon resources =class @port*(by class and device instance ID)
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[Example 12：列出设备的类的资源 @ no__t

[Example 13：按 ID @ no__t 列出远程计算机上的设备资源
