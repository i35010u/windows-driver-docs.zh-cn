---
title: DevCon 资源
description: 列出分配给指定的设备的资源。 资源是可赋值和可寻址总线路径，例如 DMA 通道、 I/O 端口、 IRQ 和内存地址。 在本地和远程计算机上有效。
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
ms.openlocfilehash: e924d4d9eb7587518eee8868ab7af09cc2af404b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547118"
---
# <a name="devcon-resources"></a>DevCon 资源


列出分配给指定的设备的资源。 资源是可赋值和可寻址总线路径，例如 DMA 通道、 I/O 端口、 IRQ 和内存地址。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] resources {* | ID [ID ...] | =class [ID [ID...]]} 
```

## <a name="span-idddkdevconresourcestoolsspanspan-idddkdevconresourcestoolsspanparameters"></a><span id="ddk_devcon_resources_tools"></span><span id="DDK_DEVCON_RESOURCES_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\**<em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和更高版本的 Windows 的计算机上，组策略默认情况下禁用远程访问服务。



<span id="______________"></span> **\\***   
表示在计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定全部或部分硬件 ID、 兼容 ID 或设备的设备实例 ID。 在指定多个 Id 时，键入一个空格之间每个 id。 包含一个 & 字符的 Id (**&**) 必须括在引号中。

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
<td align="left"><p><strong>&#39;</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义的字符串匹配 （严格按其显示）。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>&#39;* PNP0600</strong>，其中 * PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>类</em>指定设备的设备安装程序类。 等号 (**=**) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**资源**)。 否则，将忽略 DevCon **/m**参数，并显示资源分配给本地计算机上的设备而无需返回语法错误。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon resources *
devcon /m:\\server01 resources =media
devcon resources acpi* *port*
devcon resources =class port* (by class and hardware ID)
devcon resources =class @port*(by class and device instance ID)
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 12:列出资源的类的设备](devcon-examples.md#ddk_example_12_list_resources_of_a_class_of_devices_tools)

[示例 13:列出资源的 ID 的远程计算机上的设备](devcon-examples.md#ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too)









