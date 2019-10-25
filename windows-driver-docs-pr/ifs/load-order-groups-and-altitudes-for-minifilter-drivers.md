---
title: 微筛选器驱动程序的加载顺序组和等级
description: 微筛选器驱动程序的加载顺序组和等级
ms.assetid: be8f18fe-c80b-44a3-b0c3-f2f630142180
keywords:
- 海拔 WDK 文件系统微筛选器
- 加载顺序组 WDK 文件系统
- 启动类型 WDK 文件系统
- 驱动程序启动类型 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a511a319fbbbc5c24379c210d6741b6e258c5a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841140"
---
# <a name="load-order-groups-and-altitudes-for-minifilter-drivers"></a>微筛选器驱动程序的加载顺序组和等级


Windows 为在系统启动时加载的文件系统筛选器驱动程序和微筛选器驱动程序使用一组专用的加载顺序组。

旧文件系统筛选器驱动程序只能附加到现有文件系统驱动程序堆栈的顶部，并且不能附加在堆栈中间。 因此，驱动程序和加载顺序组的启动类型对旧式文件系统筛选器驱动程序很重要，因为以前的筛选器驱动程序加载后，它可以附加到文件系统驱动程序堆栈上。

首先基于驱动程序的启动类型加载驱动程序，这表示启动系统的阶段。 有关启动类型的详细信息，请参阅[确定驱动程序加载时间的内容](what-determines-when-a-driver-is-loaded.md)中的 "驱动程序启动类型"。 指定启动类型 "服务\_启动\_启动" 的所有文件系统筛选器驱动程序和微微筛选器驱动程序在启动\_系统\_启动或服务\_自动\_"启动" 的驱动程序之前加载。 启动类型由用于安装微筛选器驱动程序的 INF 文件的 ServiceInstall 部分中的**StartType**项指定。 在每个 "开始" 类型类别中，"加载顺序" 组确定何时加载文件系统筛选器驱动程序和微筛选器驱动程序。

可随时加载微筛选器驱动程序。 对于与旧式文件系统筛选器驱动程序的互操作性，筛选器驱动程序仍需要加载顺序组的概念。 每个微微筛选器驱动程序必须具有名为*海拔*的唯一标识符。 当加载微筛选器驱动程序时，微筛选器驱动程序的高度定义其相对于 i/o 堆栈中其他微筛选器驱动程序的位置。 海拔高度是被解释为十进制数的无限精度字符串。 如果微筛选器驱动程序的数字高度较低，则会将一个具有较大数值的微筛选器驱动程序加载到其下的 i/o 堆栈中。

每个加载顺序组都有一组已定义的高度。 向微筛选器驱动程序分配的高度由 Microsoft 管理。 若要请求微筛选器驱动程序的海拔高度，请发送电子邮件到 <fsfcomm@microsoft.com> 要求分配一个。

微筛选器驱动程序必须指定一个代表加载顺序组的海拔范围值。 微筛选器驱动程序的海拔值在用于安装微筛选器驱动程序的 INF 文件中的字符串部分的实例定义中指定。 还可以通过调用[**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构中的[**InstanceSetupCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)例程来指定实例定义。 可以为微筛选器驱动程序定义多个实例和高度。 这些实例定义适用于所有卷。

以下有关启动类型和加载顺序组的规则确定何时将加载微筛选器驱动程序：

-   指定特定启动类型和加载顺序组的微筛选器驱动程序将与该启动类型和加载顺序组中的其他文件系统筛选器驱动程序和微筛选器驱动程序同时加载。

-   在每个加载顺序组中，文件系统筛选器驱动程序和微微筛选器驱动程序通常按随机顺序加载。 这通常会导致基于驱动程序的安装顺序加载驱动程序。

-   如果文件系统筛选器驱动程序或微筛选器驱动程序未指定加载顺序组，则会将其加载到指定了加载顺序组的同一启动类型的所有其他驱动程序之后。

下表列出了用于微筛选器驱动程序的系统定义的负载顺序组和海拔范围。 对于每个加载顺序组，"加载顺序组" 列包含应在微筛选器的 INF 文件的 ServiceInstall 部分的**LoadOrderGroup**项中为该组指定的值。 海拔范围列包含特定加载顺序组的海拔范围。 微筛选器驱动程序必须在适当的负载顺序组或组中请求 Microsoft 的海拔分配。

请注意，"加载顺序组" 和 "高度" 范围将在堆栈上列出，这与它们的加载顺序相反。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">加载顺序组</th>
<th align="left">海拔范围</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Filter</p></td>
<td align="left"><p>420000-429999</p></td>
<td align="left"><p>此组与 Windows 2000 及更早版本上提供的筛选器加载顺序组相同。 此组最后加载，因此从文件系统中最远附加。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 顶部</p></td>
<td align="left"><p>400000-409999</p></td>
<td align="left"><p>此组适用于必须附加到所有其他 FSFilter 类型之上的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 活动监视器</p></td>
<td align="left"><p>360000-389999</p></td>
<td align="left"><p>此组包括观察和报告文件 i/o 的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 删除</p></td>
<td align="left"><p>340000-349999</p></td>
<td align="left"><p>此组包括用于恢复已删除文件的筛选器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 防病毒</p></td>
<td align="left"><p>320000-329999</p></td>
<td align="left"><p>此组包括在文件 i/o 过程中检测和杀毒病毒的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制</p></td>
<td align="left"><p>300000-309999</p></td>
<td align="left"><p>此组包括将文件数据复制到远程服务器的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 连续备份</p></td>
<td align="left"><p>280000-289999</p></td>
<td align="left"><p>此组包括将文件数据复制到备份媒体的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 内容筛选程序</p></td>
<td align="left"><p>260000-269999</p></td>
<td align="left"><p>此组包括阻止创建特定文件或文件内容的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 配额管理</p></td>
<td align="left"><p>240000-249999</p></td>
<td align="left"><p>此组包括提供增强的文件系统配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统恢复</p></td>
<td align="left"><p>220000-229999</p></td>
<td align="left"><p>此组包括执行操作以维护操作系统完整性的筛选器驱动程序，如系统还原（SR）筛选器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 群集文件系统</p></td>
<td align="left"><p>200000-209999</p></td>
<td align="left"><p>此组包括在提供跨网络的文件服务器元数据的产品中使用的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter HSM</p></td>
<td align="left"><p>180000-189999</p></td>
<td align="left"><p>此组包括执行分层存储管理的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 图像</p></td>
<td align="left"><p>170000-175000</p></td>
<td align="left"><p>此组包含可提供虚拟命名空间的类似于 ZIP 的筛选器驱动程序。</p>
<p>此加载组在 Windows Vista 和更高版本的操作系统上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 压缩</p></td>
<td align="left"><p>160000-169999</p></td>
<td align="left"><p>此组包括执行文件数据压缩的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 加密</p></td>
<td align="left"><p>140000-149999</p></td>
<td align="left"><p>此组包括在文件 i/o 过程中对数据进行加密和解密的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 虚拟化</p></td>
<td align="left"><p>130000-139999</p></td>
<td align="left"><p>此组包含虚拟化文件路径的筛选器驱动程序，如 Windows Vista 中添加的授权最少的用户（LUA）筛选器驱动程序。</p>
<p>此加载组在 Windows Vista 和更高版本的操作系统上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 物理配额管理</p></td>
<td align="left"><p>120000-129999</p></td>
<td align="left"><p>此组包括使用物理块计数来管理配额的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 打开文件</p></td>
<td align="left"><p>100000-109999</p></td>
<td align="left"><p>此组包括提供已打开文件的快照的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter Security 不得不一直</p></td>
<td align="left"><p>80000-89999</p></td>
<td align="left"><p>此组包括应用锁定和增强的访问控制列表（Acl）的筛选器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 复制保护</p></td>
<td align="left"><p>60000-69999</p></td>
<td align="left"><p>此组包括用于检查介质上的带外数据的筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 底部</p></td>
<td align="left"><p>40000-49999</p></td>
<td align="left"><p>此组是为必须附加到所有其他 FSFilter 类型的筛选器驱动程序而提供的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FSFilter 系统</p></td>
<td align="left"><p>20000-29999</p></td>
<td align="left"><p>保留供内部使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSFilter 基础结构</p></td>
<td align="left"></td>
<td align="left"><p>保留供内部使用。 此组首先加载，因此附加最接近文件系统。</p></td>
</tr>
</tbody>
</table>

 

 

 




