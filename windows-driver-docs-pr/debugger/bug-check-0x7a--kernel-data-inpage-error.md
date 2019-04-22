---
title: Bug Check 0x7A KERNEL_DATA_INPAGE_ERROR
description: KERNEL_DATA_INPAGE_ERROR bug 检查具有 0x0000007A 值。 检查此错误指示无法到内存中读取的分页文件中的内核数据请求的页面。
ms.assetid: 466d4864-8840-47b2-9a9a-302a125bf095
keywords:
- Bug Check 0x7A KERNEL_DATA_INPAGE_ERROR
- KERNEL_DATA_INPAGE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_DATA_INPAGE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c18f0ba0bdbb37f7649681218f521949eb371afd
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238798"
---
# <a name="bug-check-0x7a-kerneldatainpageerror"></a>Bug 检查 0x7A：KERNEL\_DATA\_INPAGE\_ERROR


内核\_数据\_页内\_错误 bug 检查的值为 0x0000007A。 检查此错误指示无法到内存中读取的分页文件中的内核数据请求的页面。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="kerneldatainpageerror-parameters"></a>内核\_数据\_页内\_错误参数


消息中列出的四个参数可以具有三个可能的含义。 如果第一个参数是 1 或 2 或 3 和第三个参数为 0，则参数具有以下定义。

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
<td align="left"><p>持有的时间 （1、 2 或 3） 的锁类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误状态 （通常 I/O 状态代码）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>如果锁类型为 1:</strong>当前进程</p>
<p><strong>如果锁类型为 2 或 3:</strong>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>无法呼叫到内存中的虚拟地址</p></td>
</tr>
</tbody>
</table>

 

如果第一个参数为 3 （和第三个参数为非零值） 或 4，参数具有以下定义。

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
<td align="left"><p>已保留 （3 或 4） 的锁类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误状态 （通常 I/O 状态代码）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>InPageSupport 结构的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>出错的地址</p></td>
</tr>
</tbody>
</table>

 

否则，参数具有以下定义。

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
<td align="left"><p>页表项 (PTE) 的地址的</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误状态 （通常 I/O 状态代码）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>PTE 内容</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>出错的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常情况下，可以确定该内核的原因\_数据\_页内\_错误 bug 检查从错误状态 (参数 2)。 一些常见的状态代码如下所示：

-   0xC000009A 的或状态\_不足\_资源，指示缺少非分页缓冲的池的资源。

-   0xC000009C 或状态\_设备\_数据\_错误，通常表示在硬盘上的坏扇区 （扇区）。

-   0xC000009D 或状态\_设备\_不\_已连接，指示有缺陷或松散连接电缆、 终止或控制器看不到硬盘。

-   0xC000016A 或状态\_磁盘\_操作\_失败，指示在硬盘上的坏扇区 （扇区）。

-   0xC0000185 或状态\_IO\_设备\_错误，指示不正确终止或出现故障的布线 SCSI 设备或该两个设备上尝试使用相同的 IRQ。

-   0xC000000E 或状态\_否\_SUCH\_设备，将指示硬件故障或不正确的驱动器配置。 检查您的缆线，并检查诊断实用程序，可从您的驱动器制造商的驱动器。 如果您正在使用较旧 PATA (IDE) 驱动器，此状态代码可以指示不正确的主/从驱动器配置。

这些状态代码为有特定原因最常见的。 有关可以返回其他可能的状态代码的详细信息，请参阅 Ntstatus.h 文件在 Microsoft Windows 驱动程序工具包 (WDK)。

此错误消息的另一个常见原因是出现故障的硬件或失败的 RAM。

病毒感染也会导致此 bug 检查。

<a name="resolution"></a>分辨率
----------

**解决错误的阻止问题：** I/O 状态代码为 0xC000009C 或 0xC000016A 通常指示，数据可能不会从磁盘读取因块 （扇区）。 如果该错误后，可以重新启动计算机，Autochk 自动运行，并尝试映射坏扇区中，以防止它不再使用。

如果 Autochk 不会扫描硬盘出现错误，可以手动启动磁盘扫描程序。 运行**Chkdsk /f /r**系统分区上。 磁盘扫描开始之前，必须重新启动计算机。 如果由于出现错误，无法启动计算机，使用恢复控制台并运行**Chkdsk /r**。

**警告**  系统分区已使用 FAT 文件系统格式化的如果的长文件名的 Windows 操作系统使用可能已损坏，如果使用磁盘扫描程序或基于 MS-DOS 的硬盘的另一个工具来验证的完整性从 MS-DOS 硬盘。 始终使用与你的 Windows 版本相匹配的 Chkdsk 的版本。

 

**解析有故障的硬件问题：** 如果 I/O 状态为 C0000185 且分页文件为 SCSI 磁盘上，检查磁盘电缆和 SCSI 终止的问题。

**解决失败 RAM 问题：** 运行硬件诊断系统制造商提供，尤其是内存扫描程序。 有关这些过程的详细信息，请参阅您的计算机的用户手册。

检查计算机中的所有适配器卡正确就都位。 使用墨迹橡皮擦或电力联系处理方法，可在电子用品商店，以确保适配器卡联系人是干净。

检查事件查看器中的系统日志可能有助于识别导致错误的设备的其他错误消息。 此外可以禁用内存中缓存的 BIOS 来尝试解决此错误。

请确保安装最新的 Windows Service Pack。

如果上述步骤未解决此错误，转到一个修复工具，以便诊断测试系统主板。 破裂、 污损的跟踪或在主板上的有故障组件可能导致此错误。

**解决感染病毒：** 使用任何最新的、 商业病毒扫描检查硬盘上的主启动记录的软件检查计算机有病毒。 所有 Windows 文件系统可以受到病毒都感染。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**Bug 检查 0x77 (内核\_堆栈\_页内\_错误)**](bug-check-0x77--kernel-stack-inpage-error.md)

 

 




