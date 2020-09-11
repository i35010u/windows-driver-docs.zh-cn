---
title: 文件系统筛选器驱动程序的加载顺序组
description: 文件系统筛选器驱动程序的加载顺序组
ms.assetid: 57c9e4c6-186c-464f-ac83-c0669d46b189
keywords:
- 筛选器驱动程序 WDK 文件系统，驱动程序加载
- 文件系统筛选器驱动程序 WDK，驱动程序加载
- 驱动程序加载 WDK 文件系统
- 正在加载驱动程序 WDK 文件系统
- 加载顺序组 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: febc66fcb80d008de5b0cec0795198f296bbac54
ms.sourcegitcommit: 2dd8e4262c30e3f8570e35da7b9485139b216ac8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90027558"
---
# <a name="load-order-groups-for-file-system-filter-drivers"></a>文件系统筛选器驱动程序的加载顺序组


## <span id="ddk_file_system_filter_driver_load_order_groups_if"></span><span id="DDK_FILE_SYSTEM_FILTER_DRIVER_LOAD_ORDER_GROUPS_IF"></span>


Microsoft Windows XP 和更高版本的操作系统为在系统启动时加载的文件系统筛选器驱动程序提供一组专用的加载顺序组。 在 Windows XP 之前的操作系统上，筛选器驱动程序只能使用 "筛选器" 和 "文件系统" 加载顺序组。

筛选器只能附加到现有文件系统驱动程序堆栈的顶部，并且不能附加在堆栈中间。 因此，加载顺序组对于文件系统筛选器驱动程序很重要，因为在以前的筛选器驱动程序加载时，它可以在文件系统驱动程序堆栈上附加更低的版本。

以下关于加载顺序组的规则将确定何时加载文件系统筛选器驱动程序：

-   指定特定加载顺序组的文件系统筛选器驱动程序与该组中的其他筛选器驱动程序同时加载。

-   在每个加载顺序组中，按随机顺序加载筛选器驱动程序。

-   如果文件系统筛选器驱动程序未指定加载顺序组，则将其加载到指定了加载顺序组的同一启动类型的所有其他驱动程序之后。

下表列出了文件系统筛选器驱动程序的系统定义的加载顺序组。 对于每个加载顺序组，"加载顺序组" 列包含应在筛选器 INF 文件的 "[**版本" 部分**](../install/inf-version-section.md)中的**LoadOrderGroup**条目中为该组指定的值。

请注意，加载顺序组显示在堆栈上，因为它们的加载顺序相反。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">加载顺序组</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“筛选器”</p></td>
<td align="left"><p>此组与 Windows 2000 及更早版本上提供的 "筛选器" 加载顺序组相同。 此组最后加载，因此从文件系统中最远附加。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 顶部</p></td>
<td align="left"><p>此组适用于必须附加到所有其他 FSFilter 类型之上的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 活动监视器</p></td>
<td align="left"><p>此组包括观察和报告文件 i/o 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 删除</p></td>
<td align="left"><p>此组包括用于恢复已删除文件的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 防病毒</p></td>
<td align="left"><p>此组包括在文件 i/o 过程中检测和杀毒病毒的筛选器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制</p></td>
<td align="left"><p>此组包括将文件数据复制到远程服务器的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 连续备份</p></td>
<td align="left"><p>此组包括将文件数据复制到备份媒体的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 内容筛选程序</p></td>
<td align="left"><p>此组包括阻止创建特定文件或文件内容的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 配额管理</p></td>
<td align="left"><p>此组包括提供增强的文件系统配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统恢复</p></td>
<td align="left"><p>此组包括执行操作以维护操作系统完整性的筛选器驱动程序，如系统还原 (SR) filter。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 群集文件系统</p></td>
<td align="left"><p>此组包括在提供跨网络的文件服务器元数据的产品中使用的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>此组包括执行分层存储管理的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 图像</p></td>
<td align="left"><p>此组包含可提供虚拟命名空间的类似于 ZIP 的筛选器驱动程序。</p>
<p>此加载组在 Windows Vista 和更高版本的操作系统上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 压缩</p></td>
<td align="left"><p>此组包括执行文件数据压缩的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 加密</p></td>
<td align="left"><p>此组包括在文件 i/o 过程中对数据进行加密和解密的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 虚拟化</p></td>
<td align="left"><p>此组包括用于虚拟化文件路径的筛选器驱动程序，如 Windows Vista 中添加的 (LUA) 筛选器驱动程序的最低授权用户。</p>
<p>此加载组在 Windows Vista 和更高版本的操作系统上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 物理配额管理</p></td>
<td align="left"><p>此组包括使用物理块计数来管理配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 打开文件</p></td>
<td align="left"><p>此组包括提供已打开文件的快照的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter Security 不得不一直</p></td>
<td align="left"><p>此组包括筛选器驱动程序，用于将锁定和增强的访问控制列表 (Acl) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制保护</p></td>
<td align="left"><p>此组包括用于检查介质上的带外数据的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 底部</p></td>
<td align="left"><p>此组是为必须附加到所有其他 FSFilter 类型的筛选器驱动程序而提供的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统</p></td>
<td align="left"><p>保留以供内部使用。 此组包括 HSM 和 SIS 筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 基础结构</p></td>
<td align="left"><p>保留以供内部使用。 此组首先加载，因此附加最接近文件系统。</p></td>
</tr>
</tbody>
</table>

 

 

