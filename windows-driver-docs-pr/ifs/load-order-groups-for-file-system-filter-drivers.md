---
title: 文件系统筛选器驱动程序的加载顺序组
description: 文件系统筛选器驱动程序的加载顺序组
ms.assetid: 57c9e4c6-186c-464f-ac83-c0669d46b189
keywords:
- 筛选器驱动程序 WDK 文件系统，加载的驱动程序
- 文件系统筛选器驱动程序 WDK，加载的驱动程序
- 正在加载 WDK 文件系统驱动程序
- 加载驱动程序 WDK 文件系统
- 加载顺序组 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c02f618e08d7bb3fb83aa6c53ec4fbffd6b319
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375665"
---
# <a name="load-order-groups-for-file-system-filter-drivers"></a>文件系统筛选器驱动程序的加载顺序组


## <span id="ddk_file_system_filter_driver_load_order_groups_if"></span><span id="DDK_FILE_SYSTEM_FILTER_DRIVER_LOAD_ORDER_GROUPS_IF"></span>


Microsoft Windows XP 和更高版本操作系统提供一组专用的加载顺序组的文件系统筛选器驱动程序，在系统启动时加载。 在 Windows XP 之前的操作系统，筛选器驱动程序可以使用只有"筛选器"和"文件系统"加载顺序组。

筛选器可以将附加到现有的文件系统驱动程序堆栈的顶部，并不能将附加中间堆栈。 因此，加载顺序组是重要的文件系统筛选器驱动程序，因为以前加载筛选器驱动程序，越低它可以将附加文件系统驱动程序堆栈上。

有关加载顺序组的以下规则确定何时将加载的文件系统筛选器驱动程序：

-   在该组中其他筛选器驱动程序在同一时间加载的文件系统筛选器驱动程序指定特定的加载顺序组。

-   在每个加载顺序组中，按随机顺序加载筛选器驱动程序。

-   如果文件系统筛选器驱动程序未指定加载顺序组，加载后的所有相同的其他驱动程序启动并指定加载顺序组的类型。

下表列出了文件系统筛选器驱动程序的系统定义的加载顺序组。 对于每个加载顺序组，加载顺序组列包含应为该组中指定的值**LoadOrderGroup**中的条目[**版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)筛选器的 INF 文件。

请注意，加载顺序组会列出与它们在堆栈中，这是在其中进行加载的顺序相反。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">加载顺序组</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Filter</p></td>
<td align="left"><p>此组是与"筛选器"的加载顺序组的 Windows 2000 上提供及更早版本相同。 此组上一次加载，并因此附加最远的地方文件系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 顶部</p></td>
<td align="left"><p>此组的筛选器驱动程序，必须将最重要的是附加其他 FSFilter 类型提供。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 活动监视器</p></td>
<td align="left"><p>此组包括观察并报告文件 I/O 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 撤消删除</p></td>
<td align="left"><p>此组包括恢复删除的文件的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 防病毒软件</p></td>
<td align="left"><p>此组包括检测并在文件 I/O 期间清除病毒的筛选器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制</p></td>
<td align="left"><p>此组包含文件数据复制到远程服务器的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 持续备份</p></td>
<td align="left"><p>此组包含文件数据复制到备份媒体的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 内容筛选程序</p></td>
<td align="left"><p>此组包括阻止特定文件或文件内容创建的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 配额管理</p></td>
<td align="left"><p>此组包括提供增强的文件系统配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统恢复</p></td>
<td align="left"><p>此组包含执行操作，以便保持操作系统的完整性，如系统还原 (SR) 筛选器的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 群集文件系统</p></td>
<td align="left"><p>此组包括在网络上提供文件服务器元数据的产品中使用的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>此组包括执行分层存储管理的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 映像</p></td>
<td align="left"><p>此组包括类似于 ZIP 的筛选器驱动程序提供虚拟的命名空间。</p>
<p>此负载组是操作系统的在 Windows Vista 和更高版本上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 压缩</p></td>
<td align="left"><p>此组包括执行文件的数据压缩的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 加密</p></td>
<td align="left"><p>此组包括加密和解密数据在文件 I/O 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 虚拟化</p></td>
<td align="left"><p>此组包含虚拟化的文件路径，如最低授权用户 (LUA) 筛选器驱动程序在 Windows Vista 中添加的筛选器驱动程序。</p>
<p>此负载组是操作系统的在 Windows Vista 和更高版本上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 物理配额管理</p></td>
<td align="left"><p>此组包括通过使用物理块计数来管理配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 打开文件</p></td>
<td align="left"><p>此组包括提供的已打开的文件快照的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 安全不得不</p></td>
<td align="left"><p>此组包含应用锁定的筛选器驱动程序和增强的访问控制列表 (Acl)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制保护</p></td>
<td align="left"><p>此组包括检查有介质上的带外数据的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 底部</p></td>
<td align="left"><p>必须将所有其他 FSFilter 类型下附加的筛选器驱动程序提供此组。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统</p></td>
<td align="left"><p>保留供内部使用。 此组包括 HSM 和 SIS 筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 基础结构</p></td>
<td align="left"><p>保留供内部使用。 此组加载第一次，因此附加到文件系统中最接近。</p></td>
</tr>
</tbody>
</table>

 

 

 




