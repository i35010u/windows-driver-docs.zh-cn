---
title: 权限
description: 权限
ms.assetid: 15deec90-73a3-4443-90b7-de4ec9673169
keywords:
- WDK 对象的权限
- 进程特权 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf809c5d3e84550021ad87c088347a689dda1da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568642"
---
# <a name="privileges"></a>权限


一个*特权*进程，而不是对象与关联权限。 特权的一个典型示例是**SeBackupPrivilege**，其中授予的进程备份磁盘上的文件的权限。

几个例程在完成操作之前检查当前进程的特权。 如果由系统进程执行驱动程序例程，则操作始终成功，但如果驱动程序例程不具有所需的权限的用户进程执行，然后操作可能会失败。

下表列出了权限和例程，可以要求他们成功完成一些的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>权限</th>
<th>可能需要特权的例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SeManageVolumePrivilege</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567096" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567096)"><strong>ZwSetInformationFile</strong></a> with <em>FileInformationClass</em> = <strong>FileValidDataLengthInformation</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>SeTakeOwnershipPrivilege</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563674" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563674)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SeSecurityPrivilege</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563674" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563674)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
</tbody>
</table>

 

大多数系统例程不执行任何权限检查。

 

 




