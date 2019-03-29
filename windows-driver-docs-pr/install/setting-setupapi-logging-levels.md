---
title: 设置 SetupAPI 日志记录级别
description: 设置 SetupAPI 日志记录级别
ms.assetid: e6fa4c9c-e210-42c7-8bc7-d36463073c28
keywords:
- 日志记录级别 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10bfa0dec357cf349f4f1a4ccefb1e319664e722
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348944"
---
# <a name="setting-setupapi-logging-levels"></a>设置 SetupAPI 日志记录级别





您可以控制写入到 SetupAPI 日志，无论是用于所有的信息量*设备安装应用程序*或单个设备安装应用程序。

若要更改的信息写入到的所有设备安装应用程序 SetupAPI 日志级别，请创建 （或修改） 将以下注册表值：

```cpp
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

通过设置此值 （使用下表中列出的值） 可以选择的记录的错误级别，修改的日志记录，详细级别或关闭日志记录。 此外可以对调试程序以及日志文件记录的信息。

若要指定单个设备安装应用程序的日志记录级别，请创建以下项下的注册表项：

```cpp
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\AppLogLevels
```

在此项下创建一个表示应用程序的可执行文件名称的值名称并将所需的日志记录级别分配给该名称 （使用下表中列出的值），如**service.exe=** <em>LoggingLevel</em>。

日志记录级别是一个 DWORD 值。 如果不指定此值，或为零，安装程序 Api 使用的默认行为下, 表中所示。

将 DWORD 值由三部分组成，格式为 0x 组成*SSSSDDGG*。 低 8 位，掩码 0x000000FF，由表示设置常规设备安装操作的日志记录级别。 更高的八位，表示由掩码 0x0000FF00，设置设备安装操作的日志记录级别。 最高的位均为特殊标志。

下表包含的常规日志记录级别，设备安装日志记录级别和特殊的日志记录标志适用于 Windows 2000 及更高版本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">常规日志记录级别</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>使用默认设置 (当前 0x20)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>关闭 （没有设备安装日志记录）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>记录错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>记录错误和警告。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000030</p></td>
<td align="left"><p>记录错误、 警告和其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000040</p></td>
<td align="left"><p>在详细模式中记录错误、 警告和其他信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000050</p></td>
<td align="left"><p>在详细模式下，加上时间戳的条目中记录错误、 警告和其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000060</p></td>
<td align="left"><p>在详细模式下，加上时间条目中记录错误、 警告和其他信息。 此外，所有项都都标有时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000070</p></td>
<td align="left"><p>在详细模式下，加上时间消息中记录错误、 警告和其他信息。 所有项目都均带有时间戳。 包含可能会降低系统中，如缓存命中数的其他消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x000000FF</p></td>
<td align="left"><p>指定提供的最详细日志记录。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">设备日志记录级别</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>使用默认设置 (当前 0x3000)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000100</p></td>
<td align="left"><p>关闭 （没有设备安装日志记录）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001000</p></td>
<td align="left"><p>记录错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002000</p></td>
<td align="left"><p>记录错误和警告。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00003000</p></td>
<td align="left"><p>记录错误、 警告和其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00004000</p></td>
<td align="left"><p>在详细模式中记录错误、 警告和其他信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00005000</p></td>
<td align="left"><p>在详细模式下，加上时间戳的条目中记录错误、 警告和其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00006000</p></td>
<td align="left"><p>在详细模式下，加上时间条目中记录错误、 警告和其他信息。 此外，所有项都都标有时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00007000</p></td>
<td align="left"><p>在详细模式下，加上时间消息中记录错误、 警告和其他信息。 所有项目都均带有时间戳。 包含可能会降低系统中，如缓存命中数的其他消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0000FF00</p></td>
<td align="left"><p>指定提供的最详细日志记录。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特殊标志</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x08000000</p></td>
<td align="left"><p>(<em>Windows XP 及更高版本</em>) 添加到所有日志条目的时间戳。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>(<em>Windows XP 及更高版本</em>) 的每个条目写入后不刷新到磁盘的日志记录信息。 （日志记录速度更快，但如果发生故障，系统可能会丢失信息。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>写入日志项，而对项进行分组不是按时间顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>将输出发送到调试器以及日志文件。</p></td>
</tr>
</tbody>
</table>

 

例如，安装程序 Api 解释一些示例*LoggingFlags*值，如下所示：

-   0x00000000 意味着默认日志记录。

-   0x0000FFFF 意味着详细日志记录。

-   0x8000FF00 意味着记录到日志文件和调试器详细设备安装信息。

若要修改默认 SetupAPI 日志记录级别进行全新安装时，请在文本模式下安装程序 GUI 模式下安装程序之间的时间段期间编辑注册表。 以下步骤介绍该过程。 这些步骤假定你将安装到*d:\\Winnt*并且具有相同版本的 Windows 上另一个分区的有效版本。 按如下所示更改 SetupAPI 日志记录级别：

1.  启动干净的生成要测试安装。

2.  在首次启动期间在文本模式下安装完成后停止安装过程 （即，在 GUI 模式之前安装程序）。

3.  通过选择在启动菜单中，启动进入工作版本并以管理员身份登录。

4.  查找注册表配置单元 （文件） 中*d:\\Winnt\\System32\\配置*。在这种情况下，您需要修改注册表配置单元中的*Software.sav*。

5.  在 Windows 2000 上运行*Regedt32*，选择"本地计算机的 HKEY_LOCAL_MACHINE 上"窗口中，并选择 HKEY_LOCAL_MACHINE 项。 然后单击**注册表**菜单，然后选择**加载配置单元**。

    Windows XP 及更高版本，运行*RegEdit*。 突出显示 HKEY_LOCAL_MACHINE 中，单击**文件**菜单，然后选择**加载配置单元**。

6.  浏览文件并选择*d:\\Winnt\\System32\\config\\software.sav*。 当系统提示输入密钥名称，输入"_sw.sav"

7.  打开 HKEY_LOCAL_MACHINE 下的 _sw.sav 键并突出显示以下项：

    ```cpp
    HKEY_LOCAL_MACHINE_sw.sav\Microsoft\Windows\CurrentVersion\Setup
    ```

    在 Windows 2000 中，单击**安全**菜单中，选择**权限**，并向管理员授予完全控制。

    Windows XP 及更高版本，请单击**编辑**菜单中，选择**权限**，并向管理员授予完全控制。

8.  在 Windows 2000 中，添加必要的注册表值使用上的单击此项下**编辑**，然后选择**添加值**。

    Windows XP 及更高版本，请单击**编辑**，然后选择**的新 DWORD 值**。

    输入的值。 例如，添加"0xFFFF"启用完整的详细日志记录。

9.  选择 HKEY_LOCAL_MACHINE\\_sw.sav，并卸载配置单元 (使用**注册表**Windows 2000 上的菜单或**文件**菜单在 Windows XP 及更高版本) _sw.sav 键应会消失。

10. 复制*d:\\Winnt\\System32\\config\\software.sav*到*d:\\Winnt\\System32\\配置\\软件*。

11. 重新启动并继续安装程序。

12. 若要验证此更改，在 GUI 模式下设置中，按 SHIFT + F10，然后运行*regedit.exe*并检查日志记录级别。

 

 





