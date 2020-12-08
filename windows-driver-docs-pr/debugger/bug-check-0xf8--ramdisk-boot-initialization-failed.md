---
title: Bug 检查 0xF8 RAMDISK_BOOT_INITIALIZATION_FAILED
description: RAMDISK_BOOT_INITIALIZATION_FAILED bug 检查的值为0x000000F8。 这表明尝试从 RAM 磁盘启动时出现初始化失败。
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
ms.openlocfilehash: 2c6f922f617bea4bbe0f0e8cbc7006aea788d932
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805753"
---
# <a name="bug-check-0xf8-ramdisk_boot_initialization_failed"></a>Bug 检查0xF8： RAMDISK \_ 启动 \_ 初始化 \_ 失败


RAMDISK \_ 启动 \_ 初始化 \_ 失败 bug 检查的值为0x000000F8。 这表明尝试从 RAM 磁盘启动时出现初始化失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="ramdisk_boot_initialization_failed-parameters"></a>RAMDISK \_ 启动 \_ 初始化 \_ 失败参数


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
<p><strong>1：</strong> 在加载程序内存列表中找不到 LoaderXIPRom 说明符。</p>
<p><strong>2：</strong> 无法打开 RAM 磁盘驱动程序 ( # A0 或 \Device\Ramdisk) 。</p>
<p><strong>3：</strong> FSCTL_CREATE_RAM_DISK 失败。</p>
<p><strong>4：</strong> 无法从二进制 GUID 创建 GUID 字符串。</p>
<p><strong>5：</strong> 无法创建指向 RAM 磁盘设备的符号链接。</p></td>
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

 

 

 




