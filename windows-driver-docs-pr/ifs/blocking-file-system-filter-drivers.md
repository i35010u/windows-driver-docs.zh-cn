---
title: 阻止旧版文件系统筛选器驱动程序
description: 从开始于 Windows 10，版本 1607 中，管理员和驱动程序开发人员可以使用注册表设置来阻止旧式文件系统筛选器驱动程序。
ms.assetid: 90A562FB-D616-4D38-8D4F-7EFCDF9E617F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9069f8556b9bb888400ec47d4e048c0e3d1e2ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387244"
---
# <a name="blocking-legacy-file-system-filter-drivers"></a>阻止旧版文件系统筛选器驱动程序

从开始于 Windows 10，版本 1607 中，管理员和驱动程序开发人员可以使用注册表设置来阻止旧式文件系统筛选器驱动程序。 *旧的文件系统筛选器驱动程序*是附加到文件系统的驱动程序直接堆栈，并不使用筛选器管理器。 本主题介绍阻止和解除阻止旧版的文件系统筛选器驱动程序的注册表设置。 它还介绍了旧的文件系统筛选器被阻止时输入到系统事件日志的事件以及如何检查操作系统是否有旧的文件系统驱动程序运行。

<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

## <a name="span-idhowtoblocklegacydriversspanspan-idhowtoblocklegacydriversspanspan-idhowtoblocklegacydriversspanhow-to-block-legacy-drivers"></a><span id="How_to_block_legacy_drivers"></span><span id="how_to_block_legacy_drivers"></span><span id="HOW_TO_BLOCK_LEGACY_DRIVERS"></span>如何阻止旧式驱动程序


使用**IoBlockLegacyFsFilters**注册表项以指定是否系统会阻止旧版的文件系统筛选器驱动程序。 阻止时，所有旧文件系统筛选器驱动程序无法加载。 有关注册表更改生效，执行重新启动系统。

必须在以下注册表路径下创建注册表项：

``` syntax
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\I/O System
```

有效的 DWORD 值**IoBlockLegacyFsFilters**键如下所示：

| **IoBlockLegacyFsFilters**值 | 描述                                                                                       |
|----------------------------------|---------------------------------------------------------------------------------------------------|
| **1**                            | 旧的文件系统筛选器驱动程序无法加载或将附加到存储卷。       |
| **0**                            | 旧的文件系统筛选器驱动程序不会被阻止。 在此版本中，这是默认行为。 |

 

这是密钥如下所示在注册表编辑器中：

![编辑 ioblocklegacyfsfilters 注册表项。](images/ioblockregkey.png)

## <a name="span-idexamplewhenalegacydriverisblockedfromloadingspanspan-idexamplewhenalegacydriverisblockedfromloadingspanspan-idexamplewhenalegacydriverisblockedfromloadingspanexample-when-a-legacy-driver-is-blocked-from-loading"></a><span id="Example__when__a_legacy_driver_is_blocked_from_loading"></span><span id="example__when__a_legacy_driver_is_blocked_from_loading"></span><span id="EXAMPLE__WHEN__A_LEGACY_DRIVER_IS_BLOCKED_FROM_LOADING"></span>示例： 当旧驱动程序受到阻止，无法加载


**错误**事件记录到系统事件日志时的旧文件系统筛选器驱动程序受到阻止，无法加载，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件属性</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">日志名称</td>
<td align="left">系统</td>
</tr>
<tr class="even">
<td align="left">Source</td>
<td align="left">Microsoft-Windows-Kernel-IO</td>
</tr>
<tr class="odd">
<td align="left">date</td>
<td align="left">2015 年 12 月 29 日下午 2:55:05</td>
</tr>
<tr class="even">
<td align="left">事件 ID</td>
<td align="left">1205</td>
</tr>
<tr class="odd">
<td align="left">任务类别</td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">级别</td>
<td align="left">错误</td>
</tr>
<tr class="odd">
<td align="left">关键字</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">“用户”</td>
<td align="left">CONTOSO\user</td>
</tr>
<tr class="odd">
<td align="left">计算机</td>
<td align="left">user.domain.corp.contoso.com</td>
</tr>
<tr class="even">
<td align="left">描述</td>
<td align="left">Windows 配置为阻止旧版的文件系统筛选器。 筛选器名称： \Driver\sfilter</td>
</tr>
</tbody>
</table>

 

## <a name="span-idhowtocheckiflegacydriversarerunningspanspan-idhowtocheckiflegacydriversarerunningspanspan-idhowtocheckiflegacydriversarerunningspanhow-to-check-if-legacy-drivers-are-running"></a><span id="How_to_check_if_legacy_drivers_are_running"></span><span id="how_to_check_if_legacy_drivers_are_running"></span><span id="HOW_TO_CHECK_IF_LEGACY_DRIVERS_ARE_RUNNING"></span>如何检查是否正在运行旧驱动程序


如果你不确定的哪些筛选器是旧的文件系统筛选器驱动程序或想要确保未运行，则可以执行以下：

**若要检查是否正在运行旧的文件系统筛选器驱动程序**

1.  通过右键单击打开提升的命令提示符**cmd.exe**图标，单击**以管理员身份运行**。
2.  类型： `fltmc filters`
3.  查找旧版的驱动程序，它们具有**帧**的值 **&lt;旧&gt;** 。

在此示例中，旧的文件系统的筛选器驱动程序，名为 AVLegacy 和 EncryptionLegacy，标有 **&lt;旧&gt;** 框架值。 不具有文件系统驱动程序名为 AVMiniFilter **&lt;旧版&gt;** 帧的值，因为它是一个微筛选器驱动程序 （它未直接附加到文件系统堆栈，并使用筛选器管理器）。

``` syntax
C:\Windows\system32>fltmc filters
 
Filter Name                     Num Instances    Altitude    Frame
------------------------------  -------------  ------------  -----
AVLegacy                                        389998.99   <Legacy>
EncryptionLegacy                                149998.99   <Legacy>
AVMiniFilter                           3        328000         0
```

如果您看到的阻止旧版的文件系统筛选器驱动程序后仍运行旧驱动程序，请确保在设置后重新启动系统**IoBlockLegacyFsFilters**注册表项。 该设置将会重启后的生效。

如果您的系统具有旧的文件系统筛选器驱动程序，请与各自的 Isv 以获取文件系统驱动程序的微筛选器版本。 有关移植到使用筛选器管理器模型的微筛选器驱动程序的旧文件系统筛选器驱动程序的信息，请参阅[移植旧筛选器驱动程序的指导原则](guidelines-for-porting-legacy-filter-drivers.md)。

 

 




