---
title: Bug 检查 0x2E DATA_BUS_ERROR
description: DATA_BUS_ERROR bug 检查的值为0x0000002E。 这通常表示检测到系统内存中存在奇偶校验错误。
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
ms.openlocfilehash: cc355d8b17757f75c948d60ec10c5028343718db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824679"
---
# <a name="bug-check-0x2e-data_bus_error"></a>Bug 检查0x2E：数据 \_ 总线 \_ 错误


数据 \_ 总线 \_ 错误检查的值为0x0000002E。 这通常表示检测到系统内存中存在奇偶校验错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="data_bus_error-parameters"></a>数据 \_ 总线 \_ 错误参数


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
<td align="left"><p>导致错误的物理地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>处理器状态注册 (PSR) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>错误说明注册 (杉树) </p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误通常是由硬件问题引起的，例如配置问题、硬件故障或硬件不兼容。

可能导致此错误的最常见硬件问题是内存不足、级别 2 (L2) RAM 缓存错误或视频 RAM 错误。 硬盘损坏也可能导致此错误。

如果设备驱动程序尝试访问不存在 (的 0x8 *xxxxxxx-xxxx ...* 范围中的地址，并且没有) 物理地址映射，则也可能导致此 bug 检查。

<a name="resolution"></a>解决方法
----------

**解决硬件问题：** 如果最近将硬件添加到系统中，请将其删除，查看错误是否重复出现。

如果现有硬件出现故障，请卸下或更换故障部件。 你应运行系统制造商提供的硬件诊断，以确定哪些硬件组件发生了故障。 有关这些过程的详细信息，请参阅计算机的用户手册。 检查计算机中的所有适配器卡是否都已正确安装。 使用电子用品商店提供的墨水橡皮擦或电气联系人治疗，确保适配器卡触点清晰。

如果新安装的系统出现问题，请检查 BIOS、SCSI 控制器或网卡的更新的可用性。 此类更新通常在网站或)  (硬件制造商 BBS 的公告板系统上可用。

如果在安装新的或更新的设备驱动程序之后发生错误，则应删除或替换该驱动程序。 如果在这种情况下，在启动过程中发生该错误，并使用 NTFS 格式化系统分区，则可以使用安全模式来重命名或删除有故障的驱动程序。

如果在安全模式下使用驱动程序作为系统启动过程的一部分，则需要使用恢复控制台启动计算机才能访问该文件。

对于可能帮助查明导致错误的设备或驱动程序的其他错误消息，请在事件查看器中检查系统日志。 禁用 BIOS 中的内存缓存或隐藏也可能会解决此错误。 此外，检查系统中是否存在病毒，并使用最新的商业病毒扫描软件来检查硬盘的主启动记录。 所有 Windows 文件系统都可以感染病毒。

**解决硬盘损坏问题：** 在系统分区上运行 **Chkdsk/f/r** 。 在磁盘扫描开始之前，必须重新启动系统。 如果由于错误而无法启动系统，请使用恢复控制台并运行 **Chkdsk/r**。

**警告**   如果系统分区是使用文件分配表 (FAT) 文件系统进行格式化的，则 Windows 使用的长文件名可能会损坏（如果是使用 "磁盘扫描程序" 或其他基于 Microsoft MS-DOS 的硬盘工具）来验证硬盘的完整性。 始终使用与 Windows 版本相匹配的 Chkdsk 版本。

 

 

 




