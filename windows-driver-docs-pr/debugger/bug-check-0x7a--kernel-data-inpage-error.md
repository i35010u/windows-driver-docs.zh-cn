---
title: Bug 检查 0x7A KERNEL_DATA_INPAGE_ERROR
description: KERNEL_DATA_INPAGE_ERROR bug 检查的值为0x0000007A。 此 bug 检查表明无法将页面文件中请求的内核数据页读入内存中。
keywords:
- Bug 检查 0x7A KERNEL_DATA_INPAGE_ERROR
- KERNEL_DATA_INPAGE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_DATA_INPAGE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d151c23b67b96fd190b1dc653506d86cac75cc2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831617"
---
# <a name="bug-check-0x7a-kernel_data_inpage_error"></a>Bug 检查0x7A：内核 \_ 数据 \_ INPAGE \_ 错误


内核 \_ 数据 \_ INPAGE \_ 错误 bug 检查的值为0x0000007A。 此 bug 检查表明无法将页面文件中请求的内核数据页读入内存中。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="kernel_data_inpage_error-parameters"></a>内核 \_ 数据 \_ INPAGE \_ 错误参数


消息中列出的四个参数可以有三种可能的含义。 如果第一个参数是1或2，或3，第三个参数为0，则参数具有以下定义。

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
<td align="left"><p> (1、2或3保存的锁类型) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误状态通常 (i/o 状态代码) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>如果锁类型为1：</strong> 当前进程</p>
<p><strong>如果锁类型为2或3：</strong> 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>无法分页到内存的虚拟地址</p></td>
</tr>
</tbody>
</table>

 

如果第一个参数为 3 (并且第三个参数为非零) 或4，则这些参数具有以下定义。

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
<td align="left"><p>已保留 (3 或 4) 的锁类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误状态 (通常为 i/o 状态代码) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>InPageSupport 结构的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>出错地址</p></td>
</tr>
</tbody>
</table>

 

否则，这些参数具有以下定义。

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
<td align="left"><p>页表项的地址 (PTE) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误状态通常 (i/o 状态代码) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>PTE 内容</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>出错地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常，你可以 \_ \_ \_ 从错误状态 (参数 2) 确定内核数据 INPAGE 错误 bug 检查的原因。 一些常见状态代码包括：

-   0xC000009A 或状态 \_ 资源不足 \_ ，表示缺少非分页池资源。

-   0xC000009C 或状态 \_ 设备 \_ 数据 \_ 错误通常指示硬盘)  (扇区错误。

-   0xC000009D 或状态 \_ 设备 \_ 未 \_ 连接，指示有缺陷或松动的电缆、终止，或控制器看不到硬盘。

-   0xC000016A 或 STATUS \_ DISK \_ 操作 \_ 失败，指示硬盘)  (扇区错误。

-   0xC0000185 或状态 \_ IO \_ 设备 \_ 错误表示 SCSI 设备上出现不正确的终止或故障布线，或者两个设备正在尝试使用同一 IRQ。

-   0xC000000E 或 STATUS \_ NO \_ 此类 \_ 设备表示硬件故障或驱动器配置不正确。 检查电缆，并使用驱动器制造商提供的诊断实用程序检查驱动器。 如果使用的是较旧的 PATA (IDE) 驱动器，则此状态代码可指示不正确的主/从驱动器配置。

这些状态代码是有特定原因的最常见状态代码。 有关可返回的其他可能的状态代码的详细信息，请参阅 Microsoft Windows 驱动程序工具包中的 Ntstatus .h 文件 (WDK) 。

此错误消息的另一个常见原因是硬件损坏或 RAM 发生故障。

病毒感染也可能导致此错误检查。

<a name="resolution"></a>解决方法
----------

**解决坏块问题：** 0xC000009C 或0xC000016A 的 i/o 状态代码通常指示由于坏块 (扇区) 无法从磁盘读取数据。 如果在出现错误后重新启动计算机，Autochk 会自动运行，并尝试映射坏扇区，以防止它被使用。

如果 Autochk 不扫描硬盘错误，可以手动启动磁盘扫描程序。 在系统分区上运行 **Chkdsk/f/r** 。 在磁盘扫描开始之前，必须重新启动计算机。 如果由于错误而无法启动计算机，请使用恢复控制台并运行 **Chkdsk/r**。

**警告**   如果系统分区是使用 FAT 文件系统进行格式化的，则 Windows 操作系统使用的长文件名可能会损坏，因为使用的是磁盘扫描程序或其他基于 ms-dos 的硬盘工具来验证硬盘的完整性。 始终使用与您的 Windows 版本相匹配的 Chkdsk 版本。

 

**解决硬件问题：** 如果 i/o 状态为 C0000185，且页面文件位于 SCSI 磁盘上，请检查磁盘布线和 SCSI 终止问题。

**解决失败的 RAM 问题：** 运行系统制造商提供的硬件诊断，尤其是内存扫描器。 有关这些过程的详细信息，请参阅您的计算机的所有者手册。

检查计算机中的所有适配器卡是否都已正确安装。 使用电子用品商店提供的墨水橡皮擦或电气联系人治疗，确保适配器卡触点清晰。

检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于识别导致错误的设备。 还可以禁用 BIOS 的内存缓存，尝试解决此错误。

请确保安装了最新的 Windows Service Pack。

如果前面的步骤不能解决此错误，请将系统主板用于诊断测试。 母板上的破解、有划痕的跟踪或故障组件会导致此错误。

**解决病毒感染：** 使用任意最新的商业病毒扫描软件检查计算机的病毒，以检查硬盘的主启动记录。 所有 Windows 文件系统都可以感染病毒。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Bug 检查 0x77 (内核 \_ 堆栈 \_ INPAGE \_ 错误)**](bug-check-0x77--kernel-stack-inpage-error.md)

 

 




