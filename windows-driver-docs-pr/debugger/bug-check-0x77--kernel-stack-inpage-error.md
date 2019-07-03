---
title: Bug Check 0x77 KERNEL_STACK_INPAGE_ERROR
description: KERNEL_STACK_INPAGE_ERROR bug 检查具有 0x00000077 值。 检查此错误指示无法到内存中读取的分页文件中的内核数据请求的页面。
ms.assetid: 203a6d0f-0caa-46ed-9bab-61bbde1c8016
keywords:
- Bug Check 0x77 KERNEL_STACK_INPAGE_ERROR
- KERNEL_STACK_INPAGE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_STACK_INPAGE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3a5ee531e3dd6e64921e86dbec9b405589e0102
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519208"
---
# <a name="bug-check-0x77-kernelstackinpageerror"></a>Bug 检查 0x77：内核\_堆栈\_页内\_错误


内核\_堆栈\_页内\_错误 bug 检查的值为 0x00000077。 检查此错误指示无法到内存中读取的分页文件中的内核数据请求的页面。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kernelstackinpageerror-parameters"></a>内核\_堆栈\_页内\_错误参数


消息中列出的四个参数具有两个可能的含义。

如果第一个参数为 0、 1 或 2，参数具有以下含义。

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
<td align="left"><p><strong>0:</strong>从页面缓存中检索到的内核数据页。</p>
<p><strong>1:</strong>已从磁盘中检索的页面。</p>
<p><strong>2:</strong>从磁盘检索到的页，则存储堆栈返回成功，但<strong>Status.Information</strong>不等于 PAGE_SIZE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>签名应在堆栈中显示的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>内核堆栈上的签名的地址</p></td>
</tr>
</tbody>
</table>

 

如果第一个参数为 0、 1 或 2 以外的任何值，参数具有以下含义。

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
<td align="left"><p>状态代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>I/O 状态代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>页面文件号</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>页面文件中的偏移量</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

如果第一个参数为 0 或 1，未找到内核堆栈中的堆栈签名。 此错误可能是由于有故障的硬件，例如 RAM 错误造成的。

如果第一个参数为 2，驱动程序堆栈进行的页的读取返回了不一致的状态。 例如，驱动程序堆栈返回成功状态，即使未读取整个页面也是如此。

如果第一个参数为任何值，而不是 0、 1 或 2，第一个参数的值是 NTSTATUS 错误代码，驱动程序堆栈返回后它会检索内核数据页。 您可以确定此错误的 I/O 状态代码 （第二个参数） 的确切原因。 一些常见的状态代码如下所示：

-   0xC000009A 的或状态\_不足\_资源，指示缺少非分页缓冲的池的资源。 此状态代码指示存储堆栈中的驱动程序错误。 （存储堆栈应始终能够检索此数据，而不考虑软件资源可用性。）

-   0xC000009C 或状态\_设备\_数据\_错误，指示在硬盘上的坏扇区 （扇区）。

-   0xC000009D 或状态\_设备\_不\_已连接，指示有缺陷或松散缆线、 终止或，该控制器不会看不到硬盘驱动器。

-   0xC000016A 或状态\_磁盘\_操作\_失败，指示在硬盘上的坏扇区 （扇区）。

-   0xC0000185 或状态\_IO\_设备\_错误，指示不正确终止或出现故障的布线 SCSI 设备或该两个设备上尝试使用相同的 IRQ。

这些状态代码为有特定原因最常见的。 有关可能会返回其他可能的状态代码的详细信息，请参阅 Ntstatus.h 文件在 Microsoft Windows 驱动程序工具包 (WDK)。

病毒感染也会导致此 bug 检查。

<a name="resolution"></a>分辨率
----------

**解决错误的阻止问题：** 如果该错误后，可以重新启动计算机，Autochk 自动运行，并尝试映射坏扇区中，以防止它不再使用。

如果 Autochk 不会扫描硬盘出现错误，可以手动启动磁盘扫描程序。 运行**Chkdsk /f /r**系统分区上。 磁盘扫描开始之前，必须重新启动计算机。 如果您无法启动系统，因为此错误，使用恢复控制台并运行**Chkdsk /r**。

**警告**  系统分区已使用 FAT 文件系统格式化的如果的长文件名的 Windows 操作系统使用可能已损坏，如果使用磁盘扫描程序或基于 MS-DOS 的硬盘的另一个工具来验证的完整性从 MS-DOS 在硬盘驱动器。 始终使用与你的 Windows 操作系统的版本匹配的 Chkdsk 的版本。

 

**解析有故障的硬件问题：** 如果 I/O 状态为 0xC0000185 且分页文件为 SCSI 磁盘上，检查磁盘电缆和 SCSI 终止的问题。

**解决失败 RAM 问题：** 运行硬件诊断系统制造商提供，尤其是内存扫描程序。 有关这些过程的详细信息，请参阅您的计算机的用户手册。

检查计算机中的所有适配器卡正确就都位。 使用墨迹橡皮擦或电力联系处理方法，可在电子用品商店，以确保适配器卡联系人是干净。

检查事件查看器中的系统日志可能有助于识别导致错误的设备的其他错误消息。 此外可以禁用内存中缓存的 BIOS 来尝试解决此错误。

请确保安装最新的 Windows Service Pack。

如果上述步骤无法解决该错误，请转到一个修复工具，以便诊断测试系统主板。 破裂、 污损的跟踪或在主板上的有故障组件可能导致此错误。

**解决感染病毒：** 使用任何最新的、 商业病毒扫描检查硬盘上的主启动记录的软件检查计算机有病毒。 所有 Windows 文件系统可以受到病毒都感染。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**Bug Check 0x7A (KERNEL\_DATA\_INPAGE\_ERROR)** ](bug-check-0x7a--kernel-data-inpage-error.md)

 

 




