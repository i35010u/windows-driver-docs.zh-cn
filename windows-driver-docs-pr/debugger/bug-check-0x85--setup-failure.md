---
title: Bug 检查 0x85 SETUP_FAILURE
description: SETUP_FAILURE bug 检查的值为0x00000085。 此 bug 检查表明在安装过程中出现错误。
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
ms.openlocfilehash: c19bcd50701a1ead1786ee1cba8e3a5961fad560
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819889"
---
# <a name="bug-check-0x85-setup_failure"></a>Bug 检查0x85：安装 \_ 失败


安装 \_ 失败 bug 检查的值为0x00000085。 此 bug 检查表明在安装过程中出现错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="setup_failure-parameters"></a>安装程序 \_ 失败参数


参数1指示违规类型。 未使用参数4。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>OEM HAL 字体不是有效的 fon 格式文件，因此安装程序无法显示文本。</p>
<p>此原因表明启动软盘或 CD 上<em>的 Vga fon 损坏。</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>精确的视频初始化失败：</p>
<p><strong>0： NtCreateFile</strong> of \device\video0</p>
<p><strong>1：</strong> IOCTL_VIDEO_QUERY_NUM_AVAIL_MODES</p>
<p><strong>2：</strong> IOCTL_VIDEO_QUERY_AVAIL_MODES</p>
<p><strong>3：</strong> 所需的视频模式不受支持。 此值指示内部安装错误。</p>
<p><strong>4：</strong> IOCTL_VIDEO_SET_CURRENT_MODE (无法设置视频模式) </p>
<p><strong>5：</strong> IOCTL_VIDEO_MAP_VIDEO_MEMORY</p>
<p><strong>6：</strong> IOCTL_VIDEO_LOAD_AND_SET_FONT</p></td>
<td align="left"><p>来自 NT API 调用的状态代码（如果适用）</p></td>
<td align="left"><p>视频初始化失败。</p>
<p>此失败可能表明，包含 Vga.sys (或另一个视频驱动程序适用于计算机) 的磁盘已损坏，或者该计算机有 Microsoft Windows 操作系统无法与之通信的视频硬件。</p>
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
<td align="left"><p>键盘初始化精确失败：</p>
<p><strong>0： NtCreateFile</strong> of \device\KeyboardClass0 失败。  (安装程序找不到连接到计算机的键盘。 ) </p>
<p><strong>1：</strong> 无法加载键盘布局 DLL。  (安装程序无法加载键盘布局文件。 此失败表示 CD 或软盘缺少文件，例如用于美国版本的 Kbdus.dll 或用于本地化版本的其他布局 DLL。 ) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>键盘初始化失败。</p>
<p>此失败可能表示包含键盘驱动程序 ( # A0 或 Kbdclass.sys) 的磁盘已损坏，或者计算机具有 Windows 无法与之通信的键盘硬件。 此失败还可能意味着无法加载键盘布局 DLL。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>安装程序无法解析设置开始的设备的 ARC 设备路径名称。</p>
<p>此错误是一个内部安装错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>分区健全检查失败。</p>
<p>此错误表示磁盘驱动程序中的 bug。</p>
<p></p></td>
</tr>
</tbody>
</table>

 

 

 




