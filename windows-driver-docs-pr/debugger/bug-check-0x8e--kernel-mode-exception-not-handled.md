---
title: Bug 检查 0x8E KERNEL_MODE_EXCEPTION_NOT_HANDLED
description: KERNEL_MODE_EXCEPTION_NOT_HANDLED bug 检查的值为0x0000008E。 此 bug 检查指示内核模式应用程序生成了错误处理程序未捕获的异常。
keywords:
- Bug 检查 0x8E KERNEL_MODE_EXCEPTION_NOT_HANDLED
- KERNEL_MODE_EXCEPTION_NOT_HANDLED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_MODE_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b0d54f363cd39bbd6e083c200ce43d15ea50daa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819873"
---
# <a name="bug-check-0x8e-kernel_mode_exception_not_handled"></a>Bug 检查0x8E： \_ \_ \_ 未处理内核模式 \_ 异常

\_未处理的内核模式 \_ 异常 \_ \_ bug 检查的值为0x0000008E。 此 bug 检查指示内核模式应用程序生成了错误处理程序未捕获的异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="kernel_mode_exception_not_handled-parameters"></a>内核 \_ 模式 \_ 异常 \_ 未 \_ 处理的参数


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
<td align="left"><p>未处理的异常代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>发生异常的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>捕获帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

\_未处理的内核模式 \_ 异常 \_ \_ bug 检查是一个非常常见的 bug 检查。 若要对其进行解释，必须确定生成的异常。

常见的异常代码包括：

-   数0x80000002：状态 \_ 数据类型不 \_ 一致指示遇到了未对齐的数据引用。

-   0x80000003：状态 \_ 断点指示在没有内核调试器附加到系统时遇到断点或断言。

-   0xC0000005：状态 \_ 访问 \_ 冲突表明发生了内存访问冲突。

有关异常代码的完整列表，请参阅位于 Microsoft Windows 驱动程序工具包的 inc 目录中的 Ntstatus .h 文件 (WDK) 。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
如果你不具备调试此问题的方法，则应使用一些基本的故障排除方法：

- 确保你有足够的磁盘空间。

- 如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

- 尝试更改视频适配器。

- 咨询任何 BIOS 更新的硬件供应商。

- 禁用 BIOS 内存选项，例如缓存或隐藏。

如果打算调试此问题，您可能会发现很难获得堆栈跟踪。 参数 2 (异常地址) 应标识导致此问题的驱动程序或函数。

如果发生异常代码0x80000003，则会命中硬编码断点或断言，但计算机是使用 **/NODEBUG** 开关启动的。 此问题很少发生。 如果它反复发生，请确保已连接内核调试器，并且计算机是通过 **/debug** 开关启动的。

如果发生异常代码数0x80000002，陷阱帧会提供其他信息。

如果不知道异常的具体原因，请考虑以下各项：

- 硬件不兼容。 请确保安装的任何新硬件都与安装的 Windows 版本兼容。

- 设备驱动程序或系统服务错误。 错误的设备驱动程序或系统服务可能会导致此错误。 硬件问题（例如 BIOS 不兼容、内存冲突和 IRQ 冲突）也可能生成此错误。

如果 bug 检查消息按名称列出了驱动程序，请禁用或删除该驱动程序。 同时，禁用或删除最近添加的任何驱动程序或服务。 如果在启动序列过程中出现错误，并且使用 NTFS 文件系统格式化系统分区，则可以使用安全模式来重命名或删除有故障的驱动程序。 如果在安全模式下使用驱动程序作为系统启动过程的一部分，则必须使用恢复控制台来启动计算机以访问该文件。

如果问题与 Win32k.sys 相关联，则错误源可能是第三方远程控制程序。 如果安装了此类软件，则可以通过使用恢复控制台启动系统，然后删除有问题的系统服务文件来删除此服务。

检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于识别导致 bug 检查0x8E 的设备或驱动程序。 可以禁用 BIOS 的内存缓存，尝试解决错误。 还应运行系统制造商提供的硬件诊断，尤其是内存扫描器。 有关这些过程的详细信息，请参阅您的计算机的所有者手册。

在 Windows 安装程序期间或安装完成后，可能会在首次重新启动之后出现生成此消息的错误。 此错误的可能原因是缺少用于安装的磁盘空间和系统 BIOS 不兼容性。 对于与缺少磁盘空间关联的 Windows 安装过程中出现的问题，请减少目标硬盘驱动器上的文件数。 检查并删除不需要的任何临时文件、Internet 缓存文件、应用程序备份文件以及包含磁盘扫描中保存的文件片段的 .chk 文件。 你还可以使用具有更多可用空间的另一个硬盘驱动器来安装。

