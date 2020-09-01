---
title: Wudfext.dll 中的调试程序扩展摘要
description: 本主题介绍 WudfExt.dll 中的调试程序扩展命令，你可以使用这些命令调试某些用户模式驱动程序框架 (UMDF) 驱动程序。
ms.assetid: af84ed3a-33a1-4736-9080-c43e87052064
keywords:
- UMDF 调试器扩展 WDK
- 调试器扩展 WDK UMDF
- 扩展 WDK 调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aba1594ec80d50c7a90ca7638937e6cefd3c2be0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192965"
---
# <a name="summary-of-debugger-extensions-in-wudfextdll"></a>Wudfext.dll 中的调试程序扩展摘要


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

Windows 驱动程序工具包 (WDK) 包含一个名为 " *WudfExt.dll*" 的调试器扩展库，该库位于% DDKROOT% \\ bin 子目录中。 本主题介绍 *WudfExt.dll*中的调试程序扩展命令，可用于调试用户模式驱动程序框架 (UMDF) 版本1。*x* 驱动程序。

若要调试在 UMDF 版本2.0 中启动的 UMDF 驱动程序，你必须改用 *Wdfkd.dll* 调试程序扩展库。 有关详细信息，请参阅 [**Windows Driver Framework extension ( # A0) **](../debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-.md)。

有关 *WudfExt.dll*中每个命令的完整说明，请参阅 [# A1)  ( 用户模式驱动程序框架扩展 ](../debugger/user-mode-driver-framework-extensions--wudfext-dll-.md)。 有关所有可用调试器扩展库的详细信息，请参阅 [Windows 调试](../debugger/index.md) 包附带的文档。

若要加载 *WudfExt.dll* 调试程序扩展库，请在调试器的命令提示符下输入以下命令：

**！ load WudfExt.dll**

下表总结了 WudfExt.dll 扩展库提供的扩展命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">分机</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>！帮助</strong></p></td>
<td align="left"><p>显示 WudfExt.dll 支持的所有调试器扩展</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!umdevstacks</strong></p></td>
<td align="left"><p>显示主机进程中的所有设备堆栈</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!umdevstack</strong></p></td>
<td align="left"><p>显示有关主机进程中的设备堆栈的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!umirps</strong></p></td>
<td align="left"><p>显示主机进程中挂起的 i/o 请求包的列表</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!umirp</strong></p></td>
<td align="left"><p>显示有关用户模式 i/o 请求数据包的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfdriverinfo</strong></p></td>
<td align="left"><p>显示有关 UMDF 驱动程序的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfdevicequeues</strong></p></td>
<td align="left"><p>显示设备的所有 i/o 队列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfqueue</strong></p></td>
<td align="left"><p>显示有关 i/o 队列的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfrequest</strong></p></td>
<td align="left"><p>显示有关 i/o 请求的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfobject</strong></p></td>
<td align="left"><p>显示有关 WDF 对象及其父关系和子关系的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfdevice</strong></p></td>
<td align="left"><p>显示设备即插即用 (PnP) 和电源管理状态系统</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfdumpobjects</strong></p></td>
<td align="left"><p>显示未完成的 WDF 对象的列表;用于确定驱动程序卸载时的任何泄漏对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfiotarget</strong></p></td>
<td align="left"><p>显示有关 i/o 目标的信息，包括其状态和发送请求的列表</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudffile</strong></p></td>
<td align="left"><p>显示有关框架文件的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!umfile</strong></p></td>
<td align="left"><p>显示有关 UMDF<a href="creating-a-file-object-to-handle-i-o.md" data-raw-source="[intra-stack file](creating-a-file-object-to-handle-i-o.md)">堆栈内文件的</a>信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudffilehandletarget</strong></p></td>
<td align="left"><p>显示有关基于文件句柄的 i/o 目标的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfusbtarget</strong></p></td>
<td align="left"><p>显示有关 USB i/o 目标的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfusbinterface</strong></p></td>
<td align="left"><p>显示有关 USB 接口对象的信息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>!wudfusbpipe</strong></p></td>
<td align="left"><p>显示有关 USB 管道对象的信息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>!wudfrefhist</strong></p></td>
<td align="left"><p>显示框架对象的引用计数历史记录</p></td>
</tr>
</tbody>
</table>

 

 

