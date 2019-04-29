---
title: 命令属性
description: 命令属性
ms.assetid: 8ce2c668-a130-428e-bf5f-0eab2dcd3fdb
keywords:
- 打印机属性 WDK Unidrv，命令
- WDK Unidrv 命令
- 打印机命令 WDK Unidrv，属性
- CallbackID
- Cmd
- NoPageEject
- 顺序
- 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bff0efceae5936f6a41ba19ffd2c233be0795fcc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382619"
---
# <a name="command-attributes"></a>命令属性





在指定打印机命令时，您使用属性 Unidrv 提供以下信息：

-   如果在打印机硬件中实现该操作会导致硬件来执行此操作，转义序列。

-   回调标识符和所需的参数[ **IPrintOemUni::CommandCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff554216)方法时，如果操作的实现中[呈现插件](rendering-plug-ins.md)。

-   该命令应会发送顺序，相对于其他命令。

下表列出了按字母顺序的命令属性，并介绍其参数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>CallbackID</strong></p></td>
<td><p>传递给呈现插件的正数值的值<a href="https://msdn.microsoft.com/library/windows/hardware/ff554216" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554216)"> <strong>IPrintOemUni::CommandCallback</strong> </a>方法作为其<em>dCmdCbID</em>参数。</p></td>
<td><p>所需<a href="dynamically-generated-printer-commands.md" data-raw-source="[dynamically generated printer commands](dynamically-generated-printer-commands.md)">动态生成的打印机命令</a>。 如果不是有效 <strong></em>Cmd</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>Cmd</strong></p></td>
<td><p>包含打印机命令转义序列，使用指定的文本字符串<a href="command-string-format.md" data-raw-source="[command string format](command-string-format.md)">命令字符串格式</a>。</p></td>
<td><p>必填，除非 <strong></em>CallbackID</strong>指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>NoPageEject?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否执行该命令会导致要弹出当前物理页的打印机。</p>
<p>使用仅当<strong></em>顺序</strong>指定 DOC_SETUP 部分，如果启用了双工打印功能。 若要避免双工模式文档页之间的过早页弹出，Unidrv 仅发出命令使用此属性设置为<strong>，则返回 TRUE</strong>如有可能。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>，这意味着该命令可能会导致页弹出。</p>
<p>不能<strong>，则返回 TRUE</strong>如果命令引发副作用 (即，如果该命令修改范围由命令与控制打印机设置<strong> <em>NoPageEject？</strong>设置为<strong>TRUE</strong>)。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>顺序</strong></p></td>
<td><p>部分名称和订单号，如中所述<a href="command-execution-order.md" data-raw-source="[Command Execution Order](command-execution-order.md)">命令执行顺序</a>。</p></td>
<td><p>仅对于配置命令和自定义的选项命令有效除非命令说明中另有说明。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>params</strong></p></td>
<td><p><a href="lists.md" data-raw-source="[List](lists.md)">列表</a>的<a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">标准变量</a>传递到呈现插件的 IPrintOemUni::CommandCallback 方法作为传递 EXTRAPARAM 结构中其<em>pdwParams</em>参数。</p></td>
<td><p>有效才 <strong></em>CallbackID</strong>还指定了。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




