---
title: 检查 IRP_MJ_CREATE 操作的 Oplock 状态
description: 检查 IRP_MJ_CREATE 操作的 Oplock 状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b2410294537a3367fdc5259926512a10577ad1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840733"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_create-operation"></a>检查 IRP_MJ_CREATE 操作的 Oplock 状态


以下内容仅适用于打开现有文件流 (即，新创建的流不能) 上预先存在的 oplock。

**注意**  在为任何 oplock 处理 IRP_MJ_CREATE 时，如果所需的访问权限包含除 FILE_READ_ATTRIBUTES、FILE_WRITE_ATTRIBUTES 或同步以外的任何内容，则 oplock 不会中断，除非指定了 FILE_RESERVE_OPFILTER。 如果创建成功，则指定 FILE_RESERVE_OPFILTER 始终导致 oplock 中断。 为简洁起见，下表省略了上述内容，因为它适用于所有 oplock。
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
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p> 与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 中断：</p>
<ul>
<li>
<p><b>如果</b>：<ul>
<li>
<p>已设置 FILE_RESERVE_OPFILTER 标志</p>
<p><b>OR</b></p>
</li>
<li>指定以下任何创建处置值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其它</b></p>
<ul>
<li>分解为级别2。</li>
</ul>
</li>
<li>
<p>必须先收到确认，然后才能继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>级别 2</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</li>
<li><b>与</b><ul>
<li>
<p>已设置 FILE_RESERVE_OPFILTER 标志</p>
<p><b>OR</b></p>
</li>
<li> 指定以下任何创建处置值：<ul>
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
<p>如果 oplock 中断：</p>
<ul>
<li>
<p> 中断到无。</p>
</li>
<li>
<p> 不需要确认，操作会立即继续。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Batch</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p> 与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 中断：</p>
<ul>
<li>
<p><b>如果</b>：<ul>
<li>
<p>设置了 FILE_RESERVE_OPFILTER 标志。</p>
<p><b>OR</b></p>
</li>
<li>指定以下任何创建处置值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其它</b></p>
<ul>
<li>分解为级别2。</li>
</ul>
</li>
<li>
<p>必须先收到确认，然后才能继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>筛选器</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p> 与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
<li><b>与</b><ul>
<li>
<p>在流上请求了所需的 "可写入" 的访问权限，但未打开 FILE_SHARE_READ 访问。  请注意，"可写" 访问被定义为除之外的任何属性：</p>
<ul>
<li>FILE_READ_ATTRIBUTES</li>
<li>FILE_WRITE_ATTRIBUTES</li>
<li>FILE_READ_DATA</li>
<li>FILE_READ_EA</li>
<li>FILE_EXECUTE</li>
<li>SYNCHRONIZE</li>
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
<p>如果 oplock 中断：</p>
<ul>
<li>
<p> 中断到无。</p>
</li>
<li>
<p> 必须先收到确认，然后才能继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读取</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p>与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
<li><b>与</b><ul>
<li>
<p>已设置 FILE_RESERVE_OPFILTER 标志</p>
<p><b>OR</b></p>
</li>
<li> 指定以下任何创建处置值：<ul>
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
<p>如果 oplock 中断：</p>
<ul>
<li>
<p> 中断到无。</p>
</li>
<li>
<p> 不需要确认，操作会立即继续。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Read-Handle</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p>当前打开的与现有打开的冲突，这样就会发生共享冲突。</p>
<p><b>OR</b></p>
</li>
<li>
<p>设置了 FILE_RESERVE_OPFILTER 标志。</p>
<p><b>OR</b></p>
</li>
<li>
<p>指定以下任何创建处置值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</p>
<p><b>并且</b> (以上三个条件中的任何一种) </p>
</li>
<li>
<p> 与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 中断：</p>
<ul>
<li>
<p><b>如果</b>：<ul>
<li>
<p>设置了 FILE_RESERVE_OPFILTER 标志。</p>
<p><b>OR</b></p>
</li>
<li>指定以下任何创建处置值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其它</b></p>
<ul>
<li>要读取的断点。</li>
</ul>
</li>
<li>如果 oplock 因为当前打开的与现有打开的冲突而中断，以便发生共享冲突，则必须在该操作继续之前接收确认。
      </li>
<li>如果 oplock 因任何其他原因而中断，尽管需要确认中断，但操作会立即继续 (例如，无需等待确认) 。</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Read-Write</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p>与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 中断：</p>
<ul>
<li>
<p><b>如果</b>：<ul>
<li>
<p>设置了 FILE_RESERVE_OPFILTER 标志。</p>
<p><b>OR</b></p>
</li>
<li>指定以下任何创建处置值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其它</b></p>
<ul>
<li>要读取的断点。</li>
</ul>
</li>
<li>
<p>必须先收到确认，然后才能继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读写-句柄</p>
</td>
<td>
<p>IRP_MJ_CREATE 时中断：</p>
<ul>
<li>
<p> 与所打开的 FILE_OBJECT 关联的 oplock 键不同于与拥有 oplock 的 FILE_OBJECT 相关联的 oplock 键。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 中断：</p>
<ul>
<li>
<p><b>如果</b>：<ul>
<li>
<p>设置了 FILE_RESERVE_OPFILTER 标志。</p>
<p><b>OR</b></p>
</li>
<li>指定以下任何创建处置值：<ul>
<li>FILE_SUPERSEDE</li>
<li>FILE_OVERWRITE</li>
<li>FILE_OVERWRITE_IF</li>
</ul>
</li>
</ul>
</p>
<p><b>其它</b></p>
<ul>
<li>
<p>如果当前打开的与现有打开的冲突，以便发生共享冲突，则中断到 Read-Write。  否则，中断到读取句柄。</p>
</li>
</ul>
</li>
<li>
<p>必须先收到确认，然后才能继续操作。</p>
</li>
</ul>
</td>
</tr>
</table>
 

在处理 IRP_MJ_CREATE 操作时，文件系统会为批处理和筛选器 oplock (而不是 oplock 包) 本身执行其他检查，这会影响文件系统是否要求 oplock 包执行 oplock 中断处理。 这种情况下，一个数据流上的操作可能会影响同一文件的其他数据流上的 oplock， (也就是说，以下条件列表的最后两个列表项) 。 如果满足以下一个或多个条件，则文件系统会向 oplock 包发送请求，以执行 oplock 中断处理：

-   如果这是一个已打开的网络查询并且存在 [KTM](https://go.microsoft.com/fwlink/p/?linkid=124745) 事务，则请求中断。 否则，请不要在网络查询打开时请求中断。

-   如果在备用数据流上执行了替代、覆盖或 OVERWRITE_IF 操作，并且未指定 FILE_SHARE_DELETE，并且主数据流上存在批处理或筛选器 oplock，则请求主数据流上的批处理或筛选器 oplock 中断。

-   如果在主数据流上执行了替代、覆盖或 OVERWRITE_IF 操作，并且已请求删除访问权限，并且在任何备用数据流上有批处理或筛选器 oplock，则请求批处理的中断或筛选 oplock。

当文件系统决定要求 oplock 包执行 oplock 中断处理时，将应用上表中所述的规则。

用于中断批处理和筛选器 oplock 的检查发生在进行共享访问检查之前。 这意味着批处理或筛选器 oplock 会断开，即使打开的请求最终由于共享冲突而失败。

 

 




