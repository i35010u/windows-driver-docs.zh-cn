---
title: Wudfext.dll 中的调试程序扩展摘要
description: 本主题介绍 WudfExt.dll，可用于调试某些用户模式驱动程序框架 (UMDF) 驱动程序中的调试器扩展命令。
ms.assetid: af84ed3a-33a1-4736-9080-c43e87052064
keywords:
- UMDF 调试器扩展 WDK
- 调试器扩展 WDK UMDF
- 扩展 WDK 调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bf2a50ccc369298d5427a73c0b51e3d859ff08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372169"
---
# <a name="summary-of-debugger-extensions-in-wudfextdll"></a>Wudfext.dll 中的调试程序扩展摘要


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Windows Driver Kit (WDK) 包括调试器扩展库，名为*WudfExt.dll*，位于 %DDKROOT%\\bin 子目录。 本主题介绍中的调试器扩展命令*WudfExt.dll*，可以用于调试用户模式驱动程序框架 (UMDF) 版本 1。*x*驱动程序。

若要调试 UMDF 驱动程序从 UMDF 2.0 版开始，您必须改用*Wdfkd.dll*调试器扩展库。 有关详细信息，请参阅[ **Windows 驱动程序框架扩展 (Wdfkd.dll)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。

有关在每个命令的完整说明*WudfExt.dll*，请参阅[用户模式驱动程序框架扩展 (Wudfext.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-extensions--wudfext-dll-)。 有关所有可用的调试器扩展库的详细信息，请参阅随提供的文档[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)包。

若要加载*WudfExt.dll*调试器扩展库中，输入在调试器的命令提示符下执行以下命令：

**！ 加载 WudfExt.dll**

下表总结了 WudfExt.dll 扩展插件库提供的扩展命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">扩展</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>!help</strong></p></td>
<td align="left"><p>显示所有调试器扩展 WudfExt.dll 支持</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!umdevstacks</strong></p></td>
<td align="left"><p>在主机进程显示所有设备堆栈</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!umdevstack</strong></p></td>
<td align="left"><p>显示有关设备堆栈在主机进程的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!umirps</strong></p></td>
<td align="left"><p>显示在主机进程的挂起 I/O 请求数据包的列表</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!umirp</strong></p></td>
<td align="left"><p>显示有关用户模式下 I/O 请求数据包的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfdriverinfo</strong></p></td>
<td align="left"><p>显示有关 UMDF 驱动程序的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfdevicequeues</strong></p></td>
<td align="left"><p>显示设备的所有 I/O 队列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfqueue</strong></p></td>
<td align="left"><p>显示 I/O 队列有关的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfrequest</strong></p></td>
<td align="left"><p>显示有关的 I/O 请求的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfobject</strong></p></td>
<td align="left"><p>显示有关 WDF 对象，以及其父级和子级关系的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfdevice</strong></p></td>
<td align="left"><p>显示即插即用 (PnP) 设备和设备的电源管理状态系统</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfdumpobjects</strong></p></td>
<td align="left"><p>列出可用的未完成的 WDF 对象;用于确定任何泄漏的对象，该驱动程序卸载时</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfiotarget</strong></p></td>
<td align="left"><p>显示有关的 I/O 目标，包括其状态和已发送请求的列表的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudffile</strong></p></td>
<td align="left"><p>显示框架文件有关的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!umfile</strong></p></td>
<td align="left"><p>显示有关 UMDF 信息<a href="creating-a-file-object-to-handle-i-o.md" data-raw-source="[intra-stack file](creating-a-file-object-to-handle-i-o.md)">内部堆栈文件</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudffilehandletarget</strong></p></td>
<td align="left"><p>显示基于文件句柄的 I/O 目标有关的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfusbtarget</strong></p></td>
<td align="left"><p>显示有关 USB I/O 目标的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfusbinterface</strong></p></td>
<td align="left"><p>显示有关 USB 接口对象的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfusbpipe</strong></p></td>
<td align="left"><p>显示有关 USB 的管道对象的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfrefhist</strong></p></td>
<td align="left"><p>显示引用计数的 framework 对象的历史记录</p></td>
</tr>
</tbody>
</table>

 

 

 





