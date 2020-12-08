---
title: 监视配置文件
description: 监视配置文件
keywords:
- 显示驱动程序 WDK Windows 2000，颜色管理
- 颜色管理 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000、监视器配置文件
- 监视器配置文件 WDK Windows 2000 显示
- 设备配置文件 WDK Windows 2000 显示
- 颜色空间 WDK Windows 2000 显示
- 色阶 WDK Windows 2000 显示
- 与设备无关的颜色空间 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d901365aa7d6c9e08d524fd79b7b43a2efd0f5a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792271"
---
# <a name="monitor-profiles"></a>监视配置文件


## <span id="ddk_monitor_profiles_gg"></span><span id="DDK_MONITOR_PROFILES_GG"></span>


*监视器配置文件* 是一种用于颜色管理的设备配置文件。 此配置文件包含有关如何在与设备无关的颜色空间中将监视器 *颜色空间* 和 *颜色* 范围内的颜色转换为颜色的信息。 任何用户模式应用程序（如安装程序或具有图形功能的字处理程序）都可以使用监视器配置文件，前提是 *ICM* 已启用，并且应用程序具有配置文件格式的知识。

尽管可以使用第三方工具创建自定义监视配置文件，但可以使用随 Windows 2000 和更高版本的操作系统版本一起提供的某个监视配置文件。 下表描述了这些配置文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">配置文件</th>
<th align="left">监视特征</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>mnB22G15</p></td>
<td align="left"><p>B22 phosphor，伽玛1。5</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnB22G18</p></td>
<td align="left"><p>B22 phosphor，伽玛1。8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnB22G21</p></td>
<td align="left"><p>B22 phosphor，伽玛2.1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnEBUG15</p></td>
<td align="left"><p>EBU phosphor，伽玛1。5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnEBUG18</p></td>
<td align="left"><p>EBU phosphor，伽玛1。8</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnEBUB21</p></td>
<td align="left"><p>EBU phosphor，伽玛2。1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnP22G15</p></td>
<td align="left"><p>P22 phosphor，伽玛1。5</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnP22G18</p></td>
<td align="left"><p>P22 phosphor，伽玛1。8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnP22G21</p></td>
<td align="left"><p>P22 phosphor，伽玛2。1</p></td>
</tr>
<tr class="even">
<td align="left"><p>菱形兼容 9300K G 2.2. icm</p></td>
<td align="left"><p>9300Â°开氏白点，伽玛2。2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Hitachi 兼容 9300K G 2.2. icm</p></td>
<td align="left"><p>9300Â°开氏白点，伽玛2。2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NEC 兼容 9300K G 2.2. icm</p></td>
<td align="left"><p>9300Â°开氏白点，伽玛2。2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Trinitron 兼容 9300K G 2。2</p></td>
<td align="left"><p>9300Â°开氏白点，伽玛2。2</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinstalling_a_monitor_profilespanspan-idinstalling_a_monitor_profilespanspan-idinstalling_a_monitor_profilespaninstalling-a-monitor-profile"></a><span id="Installing_a_Monitor_Profile"></span><span id="installing_a_monitor_profile"></span><span id="INSTALLING_A_MONITOR_PROFILE"></span>安装监视器配置文件

用户可以使用三种不同的方式安装监视配置文件：

1.  在 Windows 资源管理器中，选择该配置文件，右键单击该名称，然后单击 " **安装配置文件**"。

2.  请参阅 [监视器 INF 文件](monitor-inf-file-sections.md)中的配置文件。

3.  在应用程序中硬编码配置文件的路径和文件名。

由于监视配置文件的默认目录可能会发生更改，因此不建议对配置文件的路径和文件名进行硬编码。

### <a name="span-idusing_a_monitor_profilespanspan-idusing_a_monitor_profilespanspan-idusing_a_monitor_profilespanusing-a-monitor-profile"></a><span id="Using_a_Monitor_Profile"></span><span id="using_a_monitor_profile"></span><span id="USING_A_MONITOR_PROFILE"></span>使用监视器配置文件

监视器配置文件与打印机配置文件不同，它支持在输出设备和应用程序之间进行极少的通信。 例如，如果用户更改视频缓冲区中的伽玛斜坡，则不会通知监视配置文件发生此类更改。 在这种情况下，启用 ICM 后，会在图像显示之前对图像应用两种颜色更正，如下面的步骤顺序所示。

1.  该应用程序将打开并处理该映像。

2.  应用程序通过调用 Win32 GDI ICM 函数（如 **SetICMMode**）启用 ICM。 有关详细信息，请 (参阅 Microsoft Windows SDK。 ) 

3.  应用程序将图像发送到 Win32 GDI。

4.  如果启用了 ICM，Win32 GDI 将使用监视器配置文件来转换图像中的颜色。

5.  Win32 GDI 将映像发送到内核模式 GDI。

6.  内核模式 GDI 根据设备上下文的此类设备特征，为显示驱动程序设置图像的格式 (DC) 位深度、分辨率和半色调。

7.  显示驱动程序 (或视频硬件) 对图像执行伽玛更正。

 

 





