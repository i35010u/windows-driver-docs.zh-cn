---
title: 命令属性
description: 命令属性
ms.assetid: 8ce2c668-a130-428e-bf5f-0eab2dcd3fdb
keywords:
- 打印机属性 WDK Unidrv，命令
- 命令 WDK Unidrv
- 打印机命令 WDK Unidrv，属性
- CallbackID
- Cmd
- NoPageEject
- 顺序
- 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75e435cb80ca84e31c31866c9ffa308a09ea095f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842873"
---
# <a name="command-attributes"></a>命令属性





指定打印机命令时，可以使用属性为 Unidrv 提供以下信息：

-   导致硬件执行操作的转义序列（如果在打印机硬件中实现了此操作）。

-   如果在[呈现插件](rendering-plug-ins.md)中实现该操作，则为[**IPrintOemUni：： CommandCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)方法所需的回调标识符和参数。

-   命令的发送顺序，相对于其他命令。

下表按字母顺序列出了命令特性，并描述了它们的参数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>Attribute 参数</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>CallbackID</strong></p></td>
<td><p>正数值，传递给呈现插件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)"><strong>IPrintOemUni：： CommandCallback</strong></a>方法作为其<em>dCmdCbID</em>参数。</p></td>
<td><p><a href="dynamically-generated-printer-commands.md" data-raw-source="[dynamically generated printer commands](dynamically-generated-printer-commands.md)">动态生成的打印机命令</a>所必需的。 如果指定<strong></em>Cmd</strong> ，则无效。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>Cmd</strong></p></td>
<td><p>包含打印机命令转义序列的文本字符串，使用<a href="command-string-format.md" data-raw-source="[command string format](command-string-format.md)">命令字符串格式</a>指定。</p></td>
<td><p>除非指定<strong></em>CallbackID</strong> ，否则是必需的。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>NoPageEject？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，指示执行命令是否会导致打印机弹出当前物理页。</p>
<p>仅当<strong></em>顺序</strong>指定 DOC_SETUP 部分并且启用双面打印时才使用。 若要避免在 duplexed 文档页之间出现过早的页面弹出，只应在可能的情况下，Unidrv 将此特性设置为<strong>TRUE</strong>的命令发出。</p></td>
<td><p>可选。 如果未指定此参数，则默认值为<strong>FALSE</strong>，这意味着命令可能会导致页面弹出。</p>
<p>如果命令导致副作用（也就是说，如果命令将使用 <strong><em>NoPageEject？</strong> 设置为<strong>TRUE</strong>的命令修改打印机设置），则不得为<strong>true</strong> 。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>顺序</strong></p></td>
<td><p>节名称和订单号，如<a href="command-execution-order.md" data-raw-source="[Command Execution Order](command-execution-order.md)">命令执行顺序</a>中所述。</p></td>
<td><p>仅对配置命令和自定义选项命令有效，除非在命令说明中指出。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>参数</strong></p></td>
<td><p><a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">标准变量</a>的<a href="lists.md" data-raw-source="[List](lists.md)">列表</a>，传递给作为其<em>pdwParams</em>参数传递的 EXTRAPARAM 结构中的呈现插件的 IPrintOemUni：： CommandCallback 方法。</p></td>
<td><p>仅当同时指定<strong></em>CallbackID</strong>时才有效。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




