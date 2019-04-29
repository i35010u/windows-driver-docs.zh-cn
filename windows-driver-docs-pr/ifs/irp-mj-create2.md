---
title: 正在检查 IRP_MJ_CREATE 操作 Oplock 状态
description: 正在检查 IRP_MJ_CREATE 操作 Oplock 状态
ms.assetid: 30684025-9da0-4f4c-a850-ab0390bef091
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 883d03a15f8c0f8eb2a1773d4cf955d32d406b03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379699"
---
# <a name="checking-the-oplock-state-of-an-irpmjcreate-operation"></a>正在检查 IRP_MJ_CREATE 操作 Oplock 状态


以下仅适用于正在打开现有文件的流 （即，新创建的流不能对预先存在的 oplock 它们）。

**请注意**  时处理 IRP_MJ_CREATE 任何 oplock，如果所需的访问不包含任何内容 FILE_READ_ATTRIBUTES、 FILE_WRITE_ATTRIBUTES 或同步以外，机会锁不会中断 FILE_RESERVE_OPFILTER 除非指定。 始终指定 FILE_RESERVE_OPFILTER 导致破坏 oplock，如果创建成功。 为了简洁起见和简单起见下, 表中省略上述条款，因为它适用于所有 oplock。
<table>
<tr>
<th>请求类型</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>级别 1</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p> 与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p>为无中断<b>如果</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置</p>
<p><b>OR</b></p>
</li>
<li>以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其他：</b></p>
<ul>
<li>中断到级别 2。</li>
</ul>
</li>
<li>
<p>继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>级别 2</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</li>
<li><b>和：</b><ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置</p>
<p><b>OR</b></p>
</li>
<li> 以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断为无。</p>
</li>
<li>
<p> 不发送任何确认是必需的可以立即继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Batch</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p> 与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p>为无中断<b>如果</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置。</p>
<p><b>OR</b></p>
</li>
<li>以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其他：</b></p>
<ul>
<li>中断到级别 2。</li>
</ul>
</li>
<li>
<p>继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Filter</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p> 与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
<li><b>和：</b><ul>
<li>
<p>在未打开进行 FILE_SHARE_READ 访问的流上请求的"可写"所需的访问权限。  请注意，任何特性而不定义"写"访问权限：</p>
<ul>
<li>FILE_READ_ATTRIBUTES</li>
<li>FILE_WRITE_ATTRIBUTES</li>
<li>FILE_READ_DATA</li>
<li>FILE_READ_EA</li>
<li>FILE_EXECUTE</li>
<li>同步</li>
<li>READ_CONTROL</li>
</ul>
</li>
</ul>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断为无。</p>
</li>
<li>
<p> 继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Read</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p>与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
<li><b>和：</b><ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置</p>
<p><b>OR</b></p>
</li>
<li> 以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断为无。</p>
</li>
<li>
<p> 不发送任何确认是必需的可以立即继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读取句柄</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p>这样会发生共享冲突的现有打开与当前打开的冲突。</p>
<p><b>OR</b></p>
</li>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置。</p>
<p><b>OR</b></p>
</li>
<li>
<p>以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</p>
<p><b>和</b>（适用于任何上述三个条件）</p>
</li>
<li>
<p> 与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p>为无中断<b>如果</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置。</p>
<p><b>OR</b></p>
</li>
<li>以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其他：</b></p>
<ul>
<li>中断到读取。</li>
</ul>
</li>
<li>如果由于与现有的当前打开冲突打开，以便将发生共享冲突，操作破坏 oplock，继续操作之前必须收到确认。
      </li>
<li>如果 oplock 破坏出于其他原因，虽然是必需的分页符的确认，该操作将继续立即 （例如，而无需等待确认）。</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读写</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p>与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p>为无中断<b>如果</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置。</p>
<p><b>OR</b></p>
</li>
<li>以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其他：</b></p>
<ul>
<li>中断到读取。</li>
</ul>
</li>
<li>
<p>继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读写句柄</p>
</td>
<td>
<p>IRP_MJ_CREATE 上中断时：</p>
<ul>
<li>
<p> 与在其发生打开 FILE_OBJECT 关联的 oplock 键与拥有 oplock FILE_OBJECT 与关联的 oplock 密钥不同。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p>为无中断<b>如果</b>:<ul>
<li>
<p>FILE_RESERVE_OPFILTER 标志设置。</p>
<p><b>OR</b></p>
</li>
<li>以下任一创建处理设置指定的值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其他：</b></p>
<ul>
<li>
<p>如果当前打开冲突与现有打开，这样会发生共享冲突，则中断到读写。  否则，中断到读取句柄。</p>
</li>
</ul>
</li>
<li>
<p>继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
</table>
 

文件系统的批处理和筛选器 oplocks （而非 oplock 包本身） 进行其他检查时处理 IRP_MJ_CREATE 操作，这会影响是否在文件系统会要求 oplock 包来执行 oplock 中断处理。 这是其中一种数据流上的执行操作可能会影响对同一文件 （即，以下条件列表中的最后两个列表项） 的其他数据流 oplock 的用例。 如果满足一个或多个以下条件，文件系统将请求发送到 oplock 包来执行 oplock 中断处理：

-   如果这是一个开放的网络查询和请求中断[KTM](https://go.microsoft.com/fwlink/p/?linkid=124745)存在事务时。 否则，请执行的请求打开网络查询中断。

-   如果对备用数据流执行 SUPERSEDE、 覆盖或 OVERWRITE_IF 操作和未指定 FILE_SHARE_DELETE 并且对主数据的流没有批处理或筛选器 oplock，请求主数据的流上的批处理或筛选器 oplock 的中断.

-   如果 SUPERSEDE、 覆盖或 OVERWRITE_IF 操作不执行对主数据的流和已请求删除访问权限并且有批处理或筛选器 oplocks 任何备用数据流，请求对所有的备用数据批处理或筛选器 oplocks 的中断将它们的流。

当文件系统决定要求 oplock 包来执行 oplock 中断处理时上, 表中列出的规则适用。

进行共享访问检查之前，将发生中断批处理和筛选器 oplocks 的检查。 这意味着即使打开请求最终会由于共享冲突而失败，批处理或筛选器 oplock 已中断。

 

 




