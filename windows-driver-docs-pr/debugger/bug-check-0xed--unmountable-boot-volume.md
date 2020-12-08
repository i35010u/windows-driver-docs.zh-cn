---
title: Bug 检查 0xED UNMOUNTABLE_BOOT_VOLUME
description: UNMOUNTABLE_BOOT_VOLUME bug 检查的值为0x000000ED。 这表明 i/o 子系统尝试装入启动卷，但该子系统失败。
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
ms.openlocfilehash: 1498ac94bee2c7006384bc80e13686d11d76ed83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804299"
---
# <a name="bug-check-0xed-unmountable_boot_volume"></a>Bug 检查0xED：无法装入 \_ 启动 \_ 卷


"无法 \_ 启动启动 \_ 卷 bug 检查" 的值为 "0x000000ED"。 这表明 i/o 子系统尝试装入启动卷，但该子系统失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="unmountable_boot_volume-parameters"></a>无法装入 \_ 启动 \_ 卷参数


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
<td align="left"><p>文件系统中的状态代码，用于说明未能装入卷的原因</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>解决方法
----------

如果正在调试此错误，请使用！分析-v 扩展。 此扩展显示错误的相关特定于数据的错误。

此 bug 检查通常与操作系统启动存储设备（例如硬盘驱动器）的故障有关。 若要尝试验证文件系统并恢复启动记录，以下故障排除步骤可能会有所帮助。  

1. 在 Windows 10 中，使用 "故障排除" > 高级选项 "> 启动修复"。 可能需要创建可启动恢复介质，并从 USB 驱动器或 DVD 启动才能运行 Windows 恢复环境。
2. 在 Windows 恢复环境中的命令提示符下，使用 CHKDSK/r 尝试修复文件系统。  
3. 使用 bootrec 命令修复主记录和启动记录。    

如果这些步骤不成功，则可能是硬盘出现故障。 某些硬盘驱动器供应商提供的诊断工具可以帮助确认硬件故障。




 

 

 




