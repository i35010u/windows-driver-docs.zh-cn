---
title: 启用对设备安装调试的支持
description: 启用对设备安装调试的支持
ms.assetid: cc47b4c9-fd1d-47c2-9af9-0b7f4a7a918a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d52e1c40e423ef11048e05427e44de9fcb735c2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565383"
---
# <a name="enabling-support-for-debugging-device-installations"></a>启用对设备安装调试的支持


Windows vista 中，从开始，当插即用 (PnP) 管理器检测到系统中的新设备时，在操作系统启动设备安装主机进程 (*DrvInst.exe*) 若要搜索并安装设备的驱动程序。

若要设置的支持操作系统提供了用于调试设备安装主机进程的类型，创建 （或修改） 以下[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)要调试在目标系统上的注册表值：

**HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion\\设备安装程序\\DebugInstall**

下表介绍的调试支持通过使用指定的类型**DebugInstall**注册表值。

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
<td align="left"><p>将使用用户模式下调试程序调试设备安装过程。 有关详细信息，请参阅<a href="debugging-device-installations-with-a-user-mode-debugger.md" data-raw-source="[Debugging Device Installations with a User-mode Debugger](debugging-device-installations-with-a-user-mode-debugger.md)">使用用户模式下调试程序调试设备安装</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>将通过使用内核调试程序 (KD) 调试设备安装过程。 有关详细信息，请参阅<a href="debugging-device-installations-with-the-kernel-debugger--kd-.md" data-raw-source="[Debugging Device Installations with the Kernel Debugger (KD)](debugging-device-installations-with-the-kernel-debugger--kd-.md)">调试设备安装 Kernel Debugger (KD) 与</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>不进行调试的设备安装过程。 如果这是默认支持<strong>DebugInstall</strong>注册表中不存在</p></td>
</tr>
</tbody>
</table>

 

之后**DebugInstall**设置注册表值不需要重新启动你想要调试的目标系统。 但是， **DebugInstall**注册表值必须设置的下一步的设备安装和保持有效的每个后续设备安装开始之前之前的值设置为零。

**请注意**  一定要重置**DebugInstall**注册表值以零 （或删除值） 只要不再需要调试设备安装在目标系统上的。

 

 

 





