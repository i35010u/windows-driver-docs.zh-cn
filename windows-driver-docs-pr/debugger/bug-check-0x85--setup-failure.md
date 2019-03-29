---
title: Bug 检查 0x85 SETUP_FAILURE
description: SETUP_FAILURE bug 检查具有 0x00000085 值。 检查此错误指示在安装过程中出现错误。
ms.assetid: 52c93485-7c20-4a7e-8fc7-d520753973ed
keywords:
- Bug 检查 0x85 SETUP_FAILURE
- SETUP_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SETUP_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44d60422d3e0288307ad02d008f63c0907414ef7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564524"
---
# <a name="bug-check-0x85-setupfailure"></a>Bug 检查 0x85：安装程序\_失败


安装程序\_故障错误检查的值为 0x00000085。 检查此错误指示在安装过程中出现错误。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="setupfailure-parameters"></a>安装程序\_失败参数


参数 1 指示冲突的类型。 不使用参数 4。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>OEM HAL 字体不是有效.fon 格式化文件，因此安装程序无法显示文本。</p>
<p>此原因指示 Vga<em>xxx</em>.fon 上的启动软盘或 CD 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>精确视频初始化失败：</p>
<p><strong>0:NtCreateFile</strong> of \device\video0</p>
<p><strong>1:</strong>IOCTL_VIDEO_QUERY_NUM_AVAIL_MODES</p>
<p><strong>2:</strong>IOCTL_VIDEO_QUERY_AVAIL_MODES</p>
<p><strong>3:</strong>不支持所需的视频模式。 此值指示内部安装程序错误。</p>
<p><strong>4:</strong>IOCTL_VIDEO_SET_CURRENT_MODE （不能设置视频模式）</p>
<p><strong>5:</strong>IOCTL_VIDEO_MAP_VIDEO_MEMORY</p>
<p><strong>6:</strong>IOCTL_VIDEO_LOAD_AND_SET_FONT</p></td>
<td align="left"><p>中的 NT API 调用中，如果相应的状态代码</p></td>
<td align="left"><p>视频的初始化失败。</p>
<p>此失败可能表明包含 Vga.sys 的磁盘 （或另一个适用于计算机的视频驱动程序） 已损坏或计算机具有 Microsoft Windows 操作系统不能与通信的视频硬件。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>内存不足。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>精确键盘初始化失败：</p>
<p><strong>0:NtCreateFile</strong>的 \device\KeyboardClass0 失败。 （安装程序找不到连接到计算机的键盘。）</p>
<p><strong>1:</strong>无法加载 DLL 的键盘布局。 （安装程序无法加载键盘布局文件。 此故障指示 CD 或软盘缺少文件，例如美国版本或本地化版本的另一个布局 DLL Kbdus.dll。）</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>键盘初始化失败。</p>
<p>此失败可能表明包含键盘驱动程序 （I8042prt.sys 或 Kbdclass.sys） 的磁盘已损坏，或者在计算机具有键盘的硬件，Windows 无法与进行通信。 此失败可能还意味着，无法加载 DLL 的键盘布局。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>安装程序无法解析从启动的设备的设置的弧线设备路径名称。</p>
<p>此错误是内部的安装程序错误的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>分区进行健全性检查失败。</p>
<p>此错误表示磁盘驱动程序中的 bug。</p>
<p></p></td>
</tr>
</tbody>
</table>

 

 

 




