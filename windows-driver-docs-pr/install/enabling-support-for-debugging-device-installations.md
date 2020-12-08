---
title: 启用对设备安装调试的支持
description: 启用对设备安装调试的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 515bf77979658dbb5463c21136795fa5f8403281
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813175"
---
# <a name="enabling-support-for-debugging-device-installations"></a>启用对设备安装调试的支持


从 Windows Vista 开始，当即插即用 (PnP) manager 在系统中检测到新设备时，操作系统将启动设备安装主机进程 (*DrvInst.exe*) 搜索并安装设备驱动程序。

若要设置操作系统为调试设备安装主机而提供的支持类型，请在要调试的目标系统上创建 (或修改) 以下 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types) 注册表值：

**HKEY_LOCAL_MACHINE \\ SOFTWARE \\ Microsoft \\ Windows \\ CurrentVersion \\ 设备安装程序 \\ DebugInstall**

下表介绍了使用 **DebugInstall** 注册表值指定的调试支持的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DebugInstall 值</th>
<th align="left">调试支持</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>将使用用户模式调试器调试设备安装过程。 有关详细信息，请参阅 <a href="debugging-device-installations-with-a-user-mode-debugger.md" data-raw-source="[Debugging Device Installations with a User-mode Debugger](debugging-device-installations-with-a-user-mode-debugger.md)">使用用户模式调试器调试设备安装</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>将使用内核调试器 (KD) 调试设备安装过程。 有关详细信息，请参阅 <a href="debugging-device-installations-with-the-kernel-debugger--kd-.md" data-raw-source="[Debugging Device Installations with the Kernel Debugger (KD)](debugging-device-installations-with-the-kernel-debugger--kd-.md)">用内核调试器调试设备安装 (KD) </a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>无调试设备安装过程。 这是在注册表中不存在 <strong>DebugInstall</strong> 时的默认支持</p></td>
</tr>
</tbody>
</table>

 

设置 **DebugInstall** 注册表值后，你无需重新启动你要调试的目标系统。 但是，必须在下一设备安装开始之前设置 **DebugInstall** 注册表值，并对每个后续设备安装保持有效，直到将该值设置为零。

**注意**  如果不再需要在目标系统上调试设备安装，请务必将 **DebugInstall** 注册表值重置为零 (或删除该值) 。

 

 

