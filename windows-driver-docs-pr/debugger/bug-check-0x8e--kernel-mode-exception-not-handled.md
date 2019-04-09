---
title: Bug Check 0x8E KERNEL_MODE_EXCEPTION_NOT_HANDLED
description: KERNEL_MODE_EXCEPTION_NOT_HANDLED bug 检查具有 0x0000008E 值。 检查此错误指示在内核模式应用程序生成的错误处理程序未捕获异常。
ms.assetid: 987ee868-5622-44e4-979c-3ae93a98b5b1
keywords:
- Bug Check 0x8E KERNEL_MODE_EXCEPTION_NOT_HANDLED
- KERNEL_MODE_EXCEPTION_NOT_HANDLED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_MODE_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f73493b5080a2b24fdc6b0f6e4eaf10aa6c990f3
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239322"
---
# <a name="bug-check-0x8e-kernelmodeexceptionnothandled"></a>Bug 检查 0x8E：内核\_模式下\_异常\_不\_已处理


内核\_模式下\_异常\_不\_已处理错误检查的值为 0x0000008E。 检查此错误指示在内核模式应用程序生成的错误处理程序未捕获异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="kernelmodeexceptionnothandled-parameters"></a>内核\_模式下\_异常\_不\_HANDLED 参数


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
<td align="left"><p>未处理异常代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>异常发生位置的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>陷阱帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

内核\_模式下\_异常\_不\_HANDLED bug 检查是很常见的错误检查。 若要解释它，必须标识生成的异常。

常见的异常代码如下所示：

-   数 0x80000002:状态\_数据类型\_未对齐指示遇到了未对齐的数据引用。

-   0x80000003:状态\_断点指示没有内核调试器已附加到系统时，遇到断点或断言。

-   0xC0000005:状态\_访问\_冲突指示内存访问冲突发生。

异常代码的完整列表，请参阅位于 inc 目录的 Microsoft Windows Driver Kit (WDK) 中的 Ntstatus.h 文件。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。
如果您未配备调试此问题，则应使用一些基本的故障排除技巧：

-   确保你有足够的磁盘空间。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   尝试更改视频适配器。

-   咨询任何 BIOS 更新的硬件供应商。

-   禁用 BIOS 内存选项，例如缓存或隐藏。

如果您计划调试此问题，可能会发现很难获取堆栈跟踪。 驱动程序或函数导致此问题，应确定参数 2 （异常地址）。

如果出现异常代码 0x80000003，硬编码断点或断言已命中，但在此计算机启动与 **/NODEBUG**切换。 此问题很少发生。 如果重复发生，请确保内核调试器已连接并且启动计算机时与 **/debug**切换。

如果发生异常的代码数 0x80000002，陷阱框架提供的其他信息。

如果不知道特定异常的原因，请考虑以下各项：

-   硬件不兼容。 请确保已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关与 Windows 7 的兼容性信息[Windows 7 兼容性中心](https://go.microsoft.com/fwlink/p/?LinkID=246806)。

-   有故障的设备驱动程序或系统服务。 有故障的设备驱动程序或系统服务可能会导致此错误。 硬件问题，例如 BIOS 不兼容性、 内存冲突和 IRQ 冲突还可以生成此错误。

如果 bug 检查消息按名称列出了驱动程序、 禁用或删除该驱动程序。 此外，禁用或删除任何驱动程序或最近添加的服务。 如果在启动序列期间发生错误，而且使用 NTFS 文件系统格式化的系统分区，您可能能够使用安全模式下重命名或删除错误的驱动程序。 如果该驱动程序用作在安全模式下在系统启动过程的一部分，你必须使用恢复控制台访问该文件中启动计算机。

如果问题是与 Win32k.sys 相关联，错误的源可能是第三方远程控制程序。 如果安装了此类软件，您可以通过在开始使用恢复控制台，然后在删除有问题的系统服务文件系统中删除服务。

有关其他错误消息可能有助于识别设备或驱动程序导致 bug 检查 0x8e 越权检查事件查看器中的系统日志。 您可以禁用内存缓存来尝试解决该错误的 bios。 您还应运行硬件诊断，尤其是内存扫描程序，系统制造商提供。 有关这些过程的详细信息，请参阅您的计算机的用户手册。

在 Windows 安装过程中或在安装完成后，在第一重启后可能出现此错误，将生成此消息。 错误的可能原因是缺少的安装和系统 BIOS 不兼容的磁盘空间。 对于在 Windows 安装过程中与磁盘空间不足的问题，减少目标硬盘驱动器上的文件的数。 检查并删除任何不需要具有的临时文件、 Internet 缓存文件、 应用程序的备份文件和.chk 文件，其中包含从磁盘扫描保存的文件碎片。 也可以使用另一个硬盘驱动器上更多可用空间用于安装。

可以通过升级系统 BIOS 版本来解决 BIOS 问题。

 

 




