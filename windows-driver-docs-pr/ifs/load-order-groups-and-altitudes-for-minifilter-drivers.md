---
title: 加载顺序组和海拔微筛选器驱动程序的地区
description: 加载顺序组和海拔微筛选器驱动程序的地区
ms.assetid: be8f18fe-c80b-44a3-b0c3-f2f630142180
keywords:
- 海拔的地区 WDK 文件系统微筛选器
- 加载顺序组 WDK 文件系统
- 启动类型 WDK 文件系统
- 驱动程序开始类型 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bc4e23f35d2a518c5bf1e2b3a251b0d18edb6c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533347"
---
# <a name="load-order-groups-and-altitudes-for-minifilter-drivers"></a>加载顺序组和海拔微筛选器驱动程序的地区


Windows 使用的文件系统筛选器驱动程序和微筛选器驱动程序在系统启动时加载一组专用的加载顺序组。

旧的文件系统筛选器驱动程序可以将附加到现有的文件系统驱动程序堆栈的顶部，并不能将附加中间堆栈。 因此，驱动程序和加载顺序组的启动类型至关重要旧的文件系统筛选器驱动程序，因为以前加载筛选器驱动程序，越低它可以将附加文件系统驱动程序堆栈上。

第一次基于该驱动程序，它表示引导系统的各个阶段的启动类型加载驱动程序。 有关启动类型的详细信息，请参阅"驱动程序启动类型"中[确定当驱动程序加载的内容](what-determines-when-a-driver-is-loaded.md)。 所有文件系统筛选器驱动程序和指定的服务的启动类型的微筛选器驱动程序\_引导\_之前具有服务启动类型的驱动程序将加载开始\_系统\_开始或服务\_自动\_开始。 指定的启动类型**StartType** ServiceInstall 一部分用于安装微筛选器驱动程序的 INF 文件中的条目。 在开始每个类型类别中，加载顺序组确定何时将加载文件系统筛选器驱动程序和微筛选器驱动程序。

可以在任何时候加载微筛选器驱动程序。 微筛选器驱动程序的互操作性与旧的文件系统筛选器驱动程序仍需要的加载顺序组概念。 每个微筛选器驱动程序必须具有名为的唯一标识符*海拔高度*。 加载微筛选器驱动程序时，微筛选器驱动程序的海拔高度 I/O 堆栈中定义其位置相对于其他微筛选器驱动程序。 海拔高度为无限精度字符串解释为十进制数。 具有较低数字的海拔高度的微筛选器驱动程序加载到下一个微筛选器驱动程序具有更高版本的数字值的 I/O 堆栈。

每个加载顺序组已定义的范围的海拔的地区。 由 Microsoft 管理的海拔微筛选器驱动程序的地区分配。 若要请求微筛选器驱动程序的海拔高度，发送电子邮件至<fsfcomm@microsoft.com>另一个用于分配请求。

微筛选器驱动程序必须指定将在海拔高度范围表示加载顺序组中的海拔高度值。 用于安装微筛选器驱动程序 INF 文件中的字符串部分的实例定义中指定微筛选器驱动程序的海拔高度值。 此外可以对的调用中指定实例定义[ **InstanceSetupCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551096)例程中[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)结构。 为微筛选器驱动程序，可以定义多个实例和海拔的地区。 这些实例定义应用跨所有卷。

有关的以下规则启动类型并加载顺序组确定何时将加载微筛选器驱动程序：

-   指定特定的微筛选器驱动程序启动类型和其他文件系统筛选器驱动程序在同一时间在加载加载顺序组以及微筛选器驱动程序中的启动类型并加载顺序组。

-   在每个加载顺序组中，文件系统筛选器驱动程序和微筛选器驱动程序通常按随机顺序加载。 这通常会导致驱动程序正在加载基于在其中安装了驱动程序的顺序。

-   如果文件系统筛选器驱动程序或微筛选器驱动程序未指定加载顺序组，它加载所有的其他驱动程序的相同的启动类型并指定加载顺序组。

下表列出了系统定义的加载顺序组并且微筛选器驱动程序的海拔高度范围。 对于每个加载顺序组，加载顺序组列包含应为该组中指定的值**LoadOrderGroup**微筛选器的 INF 文件的 ServiceInstall 部分中的条目。 海拔高度范围列包含范围的海拔地区特定的加载顺序组。 微筛选器驱动程序必须在相应的加载顺序组或组从 Microsoft 请求的海拔高度分配。

请注意与它们在堆栈中，这是相反的顺序进行加载的顺序列出的加载顺序组和海拔高度范围。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">加载顺序组</th>
<th align="left">海拔高度范围</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Filter</p></td>
<td align="left"><p>420000-429999</p></td>
<td align="left"><p>此组是与筛选器相同加载了适用于 Windows 2000 及更早的顺序组。 此组上一次加载，并因此附加最远的地方文件系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 顶部</p></td>
<td align="left"><p>400000-409999</p></td>
<td align="left"><p>此组的筛选器驱动程序，必须将最重要的是附加其他 FSFilter 类型提供。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 活动监视器</p></td>
<td align="left"><p>360000-389999</p></td>
<td align="left"><p>此组包括观察并报告文件 I/O 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 撤消删除</p></td>
<td align="left"><p>340000-349999</p></td>
<td align="left"><p>此组包括恢复删除的文件的筛选器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 防病毒软件</p></td>
<td align="left"><p>320000-329999</p></td>
<td align="left"><p>此组包括检测并在文件 I/O 期间清除病毒的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制</p></td>
<td align="left"><p>300000-309999</p></td>
<td align="left"><p>此组包含文件数据复制到远程服务器的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 持续备份</p></td>
<td align="left"><p>280000-289999</p></td>
<td align="left"><p>此组包含文件数据复制到备份媒体的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 内容筛选程序</p></td>
<td align="left"><p>260000-269999</p></td>
<td align="left"><p>此组包括阻止特定文件或文件内容创建的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 配额管理</p></td>
<td align="left"><p>240000-249999</p></td>
<td align="left"><p>此组包括提供增强的文件系统配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统恢复</p></td>
<td align="left"><p>220000-229999</p></td>
<td align="left"><p>此组包含执行操作，以便保持操作系统的完整性，如系统还原 (SR) 筛选器的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 群集文件系统</p></td>
<td align="left"><p>200000-209999</p></td>
<td align="left"><p>此组包括在网络上提供文件服务器元数据的产品中使用的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>180000-189999</p></td>
<td align="left"><p>此组包括执行分层存储管理的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 映像</p></td>
<td align="left"><p>170000-175000</p></td>
<td align="left"><p>此组包括类似于 ZIP 的筛选器驱动程序提供虚拟的命名空间。</p>
<p>此负载组是操作系统的在 Windows Vista 和更高版本上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 压缩</p></td>
<td align="left"><p>160000-169999</p></td>
<td align="left"><p>此组包括执行文件的数据压缩的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 加密</p></td>
<td align="left"><p>140000-149999</p></td>
<td align="left"><p>此组包括加密和解密数据在文件 I/O 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 虚拟化</p></td>
<td align="left"><p>130000- 139999</p></td>
<td align="left"><p>此组包含虚拟化的文件路径，如最低授权用户 (LUA) 筛选器驱动程序在 Windows Vista 中添加的筛选器驱动程序。</p>
<p>此负载组是操作系统的在 Windows Vista 和更高版本上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 物理配额管理</p></td>
<td align="left"><p>120000-129999</p></td>
<td align="left"><p>此组包括通过使用物理块计数来管理配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 打开文件</p></td>
<td align="left"><p>100000-109999</p></td>
<td align="left"><p>此组包括提供的已打开的文件快照的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 安全不得不</p></td>
<td align="left"><p>80000-89999</p></td>
<td align="left"><p>此组包含应用锁定的筛选器驱动程序和增强的访问控制列表 (Acl)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制保护</p></td>
<td align="left"><p>60000-69999</p></td>
<td align="left"><p>此组包括检查有介质上的带外数据的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 底部</p></td>
<td align="left"><p>40000-49999</p></td>
<td align="left"><p>必须将所有其他 FSFilter 类型下附加的筛选器驱动程序提供此组。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统</p></td>
<td align="left"><p>20000-29999</p></td>
<td align="left"><p>保留供内部使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 基础结构</p></td>
<td align="left"></td>
<td align="left"><p>保留供内部使用。 此组加载第一次，因此附加到文件系统中最接近。</p></td>
</tr>
</tbody>
</table>

 

 

 




