---
title: Bug 检查 0x2E DATA_BUS_ERROR
description: DATA_BUS_ERROR bug 检查具有 0x0000002E 值。 这通常指示已检测到奇偶校验错误在系统内存中。
ms.assetid: 117adb1b-49aa-4c4e-ae01-730d1d653c02
keywords:
- Bug 检查 0x2E DATA_BUS_ERROR
- DATA_BUS_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DATA_BUS_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22b7f40eff415e705d3044fe13a13ee9182a3678
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239398"
---
# <a name="bug-check-0x2e-databuserror"></a>Bug 检查 0x2E：数据\_总线\_错误


数据\_总线\_错误 bug 检查的值为 0x0000002E。 这通常指示已检测到奇偶校验错误在系统内存中。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="databuserror-parameters"></a>数据\_总线\_错误参数


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
<td align="left"><p>导致错误的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致故障的物理地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>处理器状态寄存器 (PSR)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>出错指令寄存器 (FIR)</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

几乎总是由硬件问题-配置问题、 有故障的硬件或不兼容的硬件导致此错误。

最常见的硬件问题，可能会导致此错误是有缺陷的 RAM，级别 2 (L2) RAM 缓存错误或视频 RAM 错误。 硬盘损坏也会导致此错误。

此 bug 检查也会导致设备驱动程序尝试访问的地址在 0x8*xxxxxxx*不存在 （换句话说，不具有物理地址映射） 的范围。

<a name="resolution"></a>分辨率
----------

**解决硬件问题：** 如果硬件最近已添加到系统，则删除它才能看到如果错误重复出现。

如果现有硬件出现故障，删除或更换有故障的组件。 应运行硬件诊断以确定系统制造商提供的硬件组件已失败。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。 检查计算机中的所有适配器卡正确就都位。 使用墨迹橡皮擦或电力联系处理方法，可在电子用品商店，以确保适配器卡联系人是干净。

如果该问题发生在新安装的系统上，检查 BIOS，SCSI 控制器或网络卡可用的更新。 上的 Web 站点或硬件制造商的公告板系统 (BBS) 通常提供了这种类型的更新。

如果在安装新的或更新设备驱动程序后出现错误，应移除或替换驱动程序。 如果在启动期间该错误发生此情况下，并使用 NTFS 格式化的系统分区，您可能能够使用安全模式下重命名或删除错误的驱动程序。

如果该驱动程序用作在安全模式下在系统启动过程的一部分，您需要启动计算机才能访问该文件使用恢复控制台。

有关可能会帮助找出设备或导致错误的驱动程序的其他错误消息，检查事件查看器中的系统日志。 禁用内存缓存或 BIOS 中的隐藏操作还可能会解决此错误。 此外，检查有病毒，使用任何最新的商业病毒扫描检查硬盘上的主启动记录的软件系统。 所有 Windows 文件系统可以受到病毒都感染。

**在解决有关硬盘损坏问题：** 运行**Chkdsk /f /r**系统分区上。 磁盘扫描开始之前，必须重新启动系统。 如果由于错误，导致系统无法启动，使用恢复控制台并运行**Chkdsk /r**。

**警告**  如果磁盘扫描程序或其他 Microsoft 基于 MS-DOS 的硬盘工具用于验证，如果您的系统分区用文件分配表 (FAT) 文件系统格式化的可能损坏长文件名由 Windows从 MS-DOS 硬盘的完整性。 始终使用与你的 Windows 版本匹配的 Chkdsk 的版本。

 

 

 




