---
title: Bug 检查 0xF8 RAMDISK_BOOT_INITIALIZATION_FAILED
description: RAMDISK_BOOT_INITIALIZATION_FAILED bug 检查具有 0x000000F8 值。 这表示初始化失败尝试从 RAM 磁盘启动时出现。
ms.assetid: 73b053af-6ecb-48a3-b09d-e28d39390d11
keywords:
- Bug 检查 0xF8 RAMDISK_BOOT_INITIALIZATION_FAILED
- RAMDISK_BOOT_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RAMDISK_BOOT_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 519f19e05f81ea8ff213b489f66217e415127d5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547464"
---
# <a name="bug-check-0xf8-ramdiskbootinitializationfailed"></a>Bug 检查 0xF8:RAMDISK\_引导\_初始化\_失败


RAMDISK\_引导\_初始化\_失败错误检查的值为 0x000000F8。 这表示初始化失败尝试从 RAM 磁盘启动时出现。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="ramdiskbootinitializationfailed-parameters"></a>RAMDISK\_引导\_初始化\_失败参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>指示失败的原因。</p>
<p><strong>1:</strong>加载程序内存列表中不发现任何 LoaderXIPRom 描述符。</p>
<p><strong>2:</strong>无法打开 RAM 磁盘驱动程序 （ramdisk.sys 或 \Device\Ramdisk）。</p>
<p><strong>3:</strong>FSCTL_CREATE_RAM_DISK 失败。</p>
<p><strong>4:</strong>无法从二进制 GUID 创建 GUID 字符串。</p>
<p><strong>5:</strong>无法创建指向 RAM 磁盘设备的符号链接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>NTSTATUS 代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

 

 




