---
title: 监视配置文件
description: 监视配置文件
ms.assetid: aede7ada-3826-40a4-8b37-18ae242eea77
keywords:
- 显示驱动程序 WDK Windows 2000 中，颜色管理
- 显示颜色管理 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，监视配置文件
- 监视配置文件 WDK Windows 2000 显示
- 显示设备配置文件 WDK Windows 2000
- 颜色空间 WDK Windows 2000 显示
- 色域 WDK Windows 2000 显示
- 独立于设备的颜色空间 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75530936648e2086c9f10b02e8686c30993bc442
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525578"
---
# <a name="monitor-profiles"></a>监视配置文件


## <span id="ddk_monitor_profiles_gg"></span><span id="DDK_MONITOR_PROFILES_GG"></span>


一个*监视配置文件*是一种用于颜色管理的设备配置文件。 此配置文件包含有关如何将转换的监视器中的颜色信息*颜色空间*并*色域*到独立于设备的颜色空间中的颜色。 任何用户模式应用程序中，例如安装程序或字处理器使用图形功能，可以使用监视器的配置文件，前提是*ICM*已启用，并且该应用程序的配置文件的格式的知识。

尽管可以创建自定义监视配置文件使用第三方工具，但你可能能够使用与 Windows 2000 和更高版本的操作系统版本一起提供的监视器配置文件之一。 这些配置文件下表所述。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">配置文件</th>
<th align="left">监视器特征</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>mnB22G15.icm</p></td>
<td align="left"><p>B22 荧光，gamma 1.5</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnB22G18.icm</p></td>
<td align="left"><p>B22 荧光，gamma 1.8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnB22G21.icm</p></td>
<td align="left"><p>B22 荧光，gamma 2.1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnEBUG15.icm</p></td>
<td align="left"><p>EBU 荧光，gamma 1.5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnEBUG18.icm</p></td>
<td align="left"><p>EBU 荧光，gamma 1.8</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnEBUB21.icm</p></td>
<td align="left"><p>EBU 荧光，gamma 2.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnP22G15.icm</p></td>
<td align="left"><p>P22 荧光，gamma 1.5</p></td>
</tr>
<tr class="even">
<td align="left"><p>mnP22G18.icm</p></td>
<td align="left"><p>P22 荧光，gamma 1.8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>mnP22G21.icm</p></td>
<td align="left"><p>P22 荧光，gamma 2.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>菱形兼容 9300k G2.2.icm</p></td>
<td align="left"><p>9300Â ° Kelvin 白色点，gamma 2.2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>人： Hitachi 兼容 9300k G2.2.icm</p></td>
<td align="left"><p>9300Â ° Kelvin 白色点，gamma 2.2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NEC 兼容 9300k G2.2.icm</p></td>
<td align="left"><p>9300Â ° Kelvin 白色点，gamma 2.2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>珑兼容 9300k G2.2.icm</p></td>
<td align="left"><p>9300Â ° Kelvin 白色点，gamma 2.2</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinstallingamonitorprofilespanspan-idinstallingamonitorprofilespanspan-idinstallingamonitorprofilespaninstalling-a-monitor-profile"></a><span id="Installing_a_Monitor_Profile"></span><span id="installing_a_monitor_profile"></span><span id="INSTALLING_A_MONITOR_PROFILE"></span>安装的监视器配置文件

用户可以采用三种不同方式安装监视器配置文件：

1.  在 Windows 资源管理器，选择的配置文件中，右键单击名称，然后依次**安装配置文件**。

2.  请参阅中的配置文件[监视 INF 文件](monitor-inf-file-sections.md)。

3.  硬编码配置文件的路径和文件名中应用程序的名称。

监视配置文件的默认目录是可能发生变更，因为不建议进行硬编码配置文件的路径和文件名。

### <a name="span-idusingamonitorprofilespanspan-idusingamonitorprofilespanspan-idusingamonitorprofilespanusing-a-monitor-profile"></a><span id="Using_a_Monitor_Profile"></span><span id="using_a_monitor_profile"></span><span id="USING_A_MONITOR_PROFILE"></span>使用监视器配置文件

监视器配置文件，与不同的打印机的配置文件，支持输出设备和应用程序之间很少的通信。 例如，如果用户更改了视频缓冲区中的伽玛入口，监视器配置文件不通知已发生此类更改。 在这种情况下，使用启用的 ICM，两个颜色更正应用于映像之前显示它，则以下一系列步骤中所示。

1.  应用程序打开，然后操作该映像。

2.  应用程序通过调用 Win32 GDI ICM 函数，使 ICM 如**SetICMMode**。 （请参阅 Microsoft Windows SDK for 的详细信息。）

3.  应用程序将映像发送到 Win32 GDI。

4.  如果启用了 ICM，Win32 GDI 使用显示器配置文件转换中图像的颜色。

5.  Win32 GDI 将映像发送到内核模式 GDI。

6.  内核模式 GDI 设置显示器驱动程序，根据设备上下文 (DC) 的位深度、 分辨率和半色调作为此类设备特征的图像的格式。

7.  显示驱动程序 （或视频硬件） 执行到图像的灰度校正。

 

 





