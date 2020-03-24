---
title: PnPUtil
description: PnPUtil
ms.assetid: 3678fd41-c3ee-4538-b783-6f099ac104a6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9d3487b8b43407bd3050888960d9581ca4ce4c2
ms.sourcegitcommit: 4058fcb136cfb8255ca7bec68e8597c89f7b68cd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80080132"
---
# <a name="pnputil"></a>PnPUtil


PnPUtil （PnPUtil）是一种命令行工具，可让管理员对[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)执行操作。  示例包括：

-   将驱动程序包添加到[驱动程序存储区](https://docs.microsoft.com/windows-hardware/drivers/install/driver-store)。

-   在计算机上安装驱动程序包。

-   从驱动程序存储区中删除驱动程序包。

-   枚举当前位于驱动程序存储区中的驱动程序包。 仅列出非内置包的驱动程序包。 *内置*驱动程序包是 Windows 或其 service pack 的默认安装中包含的程序包。

有关所有支持的操作的列表，请参阅[PnP 命令语法](https://review.docs.microsoft.com/en-us/windows-hardware/drivers/devtest/pnputil-command-syntax)。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以下载 PnPUtil？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PnPUtil （PnPUtil）包含在 Windows Vista （在%windir%\system32 目录下）中的每个版本中。 没有单独的 PnPUtil 下载包。</p>
<ul>
<li>打开 "<strong>命令提示符</strong>" 窗口（<strong>以管理员身份运行</strong>）。</li>
<li>键入<strong>pnputil/？</strong> 查看命令选项。 有关详细信息，请参阅<a href="pnputil-command-syntax.md" data-raw-source="[&lt;strong&gt;PnPUtil Command Syntax&lt;/strong&gt;](pnputil-command-syntax.md)"><strong>PnPUtil 命令语法</strong></a>。</li>
</ul>
<div class="alert">
<strong>注意</strong> Windows Vista 和更高版本的 Windows 上支持 PnPUtil。 PnPUtil 不适用于 Windows XP，但你可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines" data-raw-source="[Driver Install Frameworks (DIFx)](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)">驱动程序安装框架（DIFx）</a>工具来创建和自定义驱动程序包的安装。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

本部分包括以下内容：

[PnPUtil 命令语法](pnputil-command-syntax.md)

[PnPUtil 示例](pnputil-examples.md)

 

 





