---
title: 设置 SetupAPI 日志记录级别
description: 设置 SetupAPI 日志记录级别
keywords:
- 日志记录级别 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa72dbc73f67e46cdd83013e5a184e15568e07e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816673"
---
# <a name="setting-setupapi-logging-levels"></a>设置 SetupAPI 日志记录级别





可以控制写入 Setupapi.log 日志的信息量，无论是针对所有 *设备安装应用程序* 还是单个设备安装应用程序。

若要更改写入到 Setupapi.log 日志中的所有设备安装应用程序的信息级别，请创建 (或修改) 以下注册表值：

```cpp
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

通过使用) 下表中列出的值 (设置此值，你可以选择所记录的错误级别，修改日志记录的详细级别，或关闭日志记录。 还可以将信息记录到调试器以及日志文件中。

若要为单个设备安装应用程序指定日志记录级别，请在以下注册表项下创建一个注册表项：

```cpp
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\AppLogLevels
```

在此项下，创建一个表示应用程序可执行文件名称的值名称，并使用下表中列出的值将所需的日志记录级别分配给该名称 () ，如 **service.exe=**<em>logginglevel.information</em>。

日志记录级别为 DWORD 值。 如果未指定此值或此值为零，则 Setupapi.log 将使用默认行为，如下表所示。

DWORD 值由三个部分组成，格式为 0x *SSSSDDGG*。 掩码0x000000FF 表示的低8位，设置常规设备安装操作的日志记录级别。 接下来的8位（由掩码0x0000FF00 表示）设置设备安装操作的日志记录级别。 最高位是特殊标志。

下表包含 Windows 2000 和更高版本的一般日志记录级别、设备安装日志记录级别和特殊日志记录标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">一般日志记录级别</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p> (当前 0x20) 使用默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>禁用 (没有设备安装日志) 。</p></td>
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
<td align="left"><p>记录错误、警告和其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000040</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000050</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息以及时间戳条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000060</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息以及时间条目。 此外，所有条目都带有时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000070</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息以及时间消息。 所有条目都带有时间戳。 包括可能会减慢系统速度的其他消息，如缓存命中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x000000FF</p></td>
<td align="left"><p>指定最详细的日志记录。</p></td>
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
<td align="left"><p> (当前 0x3000) 使用默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000100</p></td>
<td align="left"><p>禁用 (没有设备安装日志) 。</p></td>
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
<td align="left"><p>记录错误、警告和其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00004000</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00005000</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息以及时间戳条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00006000</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息以及时间条目。 此外，所有条目都带有时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00007000</p></td>
<td align="left"><p>在详细模式下记录错误、警告和其他信息以及时间消息。 所有条目都带有时间戳。 包括可能会减慢系统速度的其他消息，如缓存命中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0000FF00</p></td>
<td align="left"><p>指定最详细的日志记录。</p></td>
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
<td align="left"><p> (<em>WINDOWS XP 和更高版本</em>) 为所有日志条目添加时间戳。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000000</p></td>
<td align="left"><p> (<em>WINDOWS XP 及更高版本</em>) 写入每个条目后，不将日志记录信息刷新到磁盘。  (日志记录的速度更快，但如果系统崩溃，则信息可能丢失。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>按时间顺序而不是对条目进行分组。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>将输出发送到调试器以及日志文件。</p></td>
</tr>
</tbody>
</table>

 

例如，Setupapi.log 解释一些示例 *LoggingFlags* 值，如下所示：

-   0x00000000 表示默认日志记录。

-   0x0000FFFF 表示详细日志记录。

-   0x8000FF00 表示日志文件和调试器的日志详细设备安装信息。

若要在全新安装期间修改默认 Setupapi.log 日志记录级别，请在文本模式安装和 GUI 模式安装之间的时间段内编辑注册表。 以下步骤介绍了该过程。 这些步骤假设你要安装到 *D： \\ Winnt* ，并在另一个分区上具有相同版本的 Windows 的有效版本。 更改 Setupapi.log 日志记录级别，如下所示：

1.  开始安装要测试的清理生成。

2.  在文本模式安装程序之后的第一次启动时，停止安装过程， (即在 GUI 模式安装) 之前。

3.  从 "启动" 菜单中选择 "启动"，然后以管理员身份登录到工作生成。

4.  在 *D： \\ Winnt \\ System32 \\ config* 中查找)  (文件的注册表配置单元。在这种情况下，需要修改 *sav* 中的注册表配置单元。

5.  在 Windows 2000 上，运行 *Regedt32*，选择 "本地计算机上的 HKEY_LOCAL_MACHINE" 窗口，并选择 HKEY_LOCAL_MACHINE 密钥。 然后单击 " **注册表** " 菜单并选择 " **加载配置单元**"。

    在 Windows XP 和更高版本上，运行 *RegEdit*。 突出显示 HKEY_LOCAL_MACHINE，单击 " **文件** " 菜单，然后选择 " **加载配置单元**"。

6.  浏览文件，然后选择 " *D： \\ Winnt \\ System32 \\ config \\ sav*"。 当系统提示输入密钥名称时，输入 _sw "sav"

7.  打开 HKEY_LOCAL_MACHINE 下的 _sw sav 项，并突出显示以下项：

    ```cpp
    HKEY_LOCAL_MACHINE_sw.sav\Microsoft\Windows\CurrentVersion\Setup
    ```

    在 Windows 2000 上，单击 " **安全** " 菜单，选择 "权限"，并向管理员授予 "完全控制" **权限**。

    在 Windows XP 和更高版本上，单击 " **编辑** " 菜单，选择 "权限"，并向管理员授予 "完全控制" **权限**。

8.  在 Windows 2000 上，单击 " **编辑** " 并选择 " **添加值**"，在此项下添加所需的注册表值。

    在 Windows XP 和更高版本中，单击 " **编辑** " 并选择 " **新建 DWORD 值**"。

    输入值。 例如，添加 "0xFFFF" 可以启用完整的详细日志记录。

9.  选择 HKEY_LOCAL_MACHINE \\ _sw ""，然后使用 windows 2000 上的 " **注册表** " 菜单或 windows XP 和更高版本上的 "文件" 菜单上的 " **文件** " 菜单卸载 hive (，) _sw. sav 密钥会消失。

10. 将 *d： \\ winnt \\ system32 \\ Config \\ sav* 复制到 *d： \\ winnt \\ system32 \\ config \\ 软件*。

11. 重新启动并继续安装。

12. 若要验证此更改，请按 GUI 模式安装程序中的 SHIFT + F10，然后运行 *regedit.exe* 并检查日志记录级别。

 

 





