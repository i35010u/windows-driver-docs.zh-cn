---
title: Bug 检查 0xED UNMOUNTABLE_BOOT_VOLUME
description: UNMOUNTABLE_BOOT_VOLUME bug 检查具有遇到 0x000000ED 值。 这表明 I/O 子系统试图装入引导卷和它失败。
ms.assetid: 7c4ab301-f110-4fc8-9ff8-242e0d2155fd
keywords:
- Bug 检查 0xED UNMOUNTABLE_BOOT_VOLUME
- UNMOUNTABLE_BOOT_VOLUME
ms.date: 06/26/2017
topic_type:
- apiref
api_name:
- UNMOUNTABLE_BOOT_VOLUME
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9dc3195969d7ce4895d3f12559fa4ffedabd18eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323171"
---
# <a name="bug-check-0xed-unmountablebootvolume"></a>Bug 检查 0xED：之后\_启动\_卷


UNMOUNTABLE\_启动\_卷 bug 检查的值为遇到 0x000000ED。 这表明 I/O 子系统试图装入引导卷和它失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="unmountablebootvolume-parameters"></a>之后\_启动\_卷参数


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
<td align="left"><p>启动卷的设备对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>描述失败原因将卷装载文件系统中的状态代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>分辨率
----------

如果要调试此错误，使用 ！ 分析-v 扩展。 此扩展显示相关数据的特定错误的错误。

检查此错误通常与 OS 引导存储设备，如硬盘驱动器故障。 若要尝试验证文件系统和恢复启动记录以下故障排除步骤可能会有所帮助。  

1. 在 Windows 10 中，使用故障排除 > 高级选项 > 启动修复。 您可能需要从 USB 驱动器或 DVD，以便运行 Windows 恢复环境中创建可启动故障恢复介质和启动。
2. 从 Windows 恢复环境中的命令提示符下使用 CHKDSK /r 尝试修复文件系统。  
3. 使用 bootrec 命令修复 master 和启动记录。    

如果这些步骤不成功就可以硬盘出现故障。 某些硬盘驱动器供应商提供可帮助确认硬件故障的诊断工具。




 

 

 




