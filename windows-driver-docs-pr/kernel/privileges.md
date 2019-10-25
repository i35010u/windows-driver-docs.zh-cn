---
title: 权限
description: 权限
ms.assetid: 15deec90-73a3-4443-90b7-de4ec9673169
keywords:
- 权限 WDK 对象
- 处理特权 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a9682cae3c6d012df4e4dd3d3c4f5ea79ba8fbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827589"
---
# <a name="privileges"></a>权限


*权限*是与进程关联的权限，而不是与对象关联的权限。 权限的典型示例是**SeBackupPrivilege**，它在某个进程上授予备份磁盘上的文件。

在完成操作之前，有几个例程检查当前进程的权限。 如果驱动程序例程由系统进程执行，则操作始终会成功，但如果驱动程序例程由没有所需权限的用户进程执行，则操作可能会失败。

下表列出了一些权限和例程的一些示例，它们可以要求它们成功。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>权限</th>
<th>可能需要权限的例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SeManageVolumePrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)"><strong>ZwSetInformationFile</strong></a> with <em>FileInformationClass</em> = <strong>FileValidDataLengthInformation</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>SeTakeOwnershipPrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SeSecurityPrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
</tbody>
</table>

 

大多数系统例程不执行任何权限检查。

 

 




