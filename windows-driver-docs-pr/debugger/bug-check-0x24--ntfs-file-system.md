---
title: Bug 检查 0x24 NTFS_FILE_SYSTEM
description: NTFS_FILE_SYSTEM bug 检查的值为0x00000024。 这表明 ntfs.sys 中出现问题，该驱动程序文件允许系统读写 NTFS 驱动器。
keywords:
- Bug 检查 0x24 NTFS_FILE_SYSTEM
- NTFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NTFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6324e9edb0dd3f5745d52273d9ebc6aa215ef6f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839805"
---
# <a name="bug-check-0x24-ntfs_file_system"></a>Bug 检查0x24： NTFS \_ 文件 \_ 系统


NTFS \_ 文件 \_ 系统 bug 检查的值为0x00000024。 这表明 ntfs.sys 中出现问题，该驱动程序文件允许系统读写 NTFS 驱动器。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="ntfs_file_system-parameters"></a>NTFS \_ 文件 \_ 系统参数


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
<td align="left"><p>指定源文件和行号信息。 高16位 ("0x" 后的前四个十六进制数字 ) 按其标识符号识别源文件。 低16位标识文件中发生错误检查的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果 <strong>NtfsExceptionFilter</strong> 位于堆栈上，则此参数指定异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果 <strong>NtfsExceptionFilter</strong> 位于堆栈上，则此参数指定上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误检查的一个可能原因是磁盘损坏。 NTFS 文件系统损坏或硬盘上的坏块 (扇区) 会导致此错误。 损坏的硬盘驱动器 (SATA/IDE) 驱动程序也可能对系统读写磁盘的能力产生负面影响，从而导致错误。

<a name="resolution"></a>解决方法
----------

**若要调试此问题：** 使用参数 3 [**(显示上下文记录)**](-cxr--display-context-record-.md) 命令，然后使用 [**Kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**解决磁盘损坏问题：**

-   事件查看器检查 "系统" 日志中显示的与硬盘驱动器相关的错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。

-   尝试禁用持续监视系统的任何病毒扫描程序、备份程序或磁盘碎片整理程序工具。

-   还应运行系统制造商提供的与存储子系统相关的硬件诊断。

-   使用扫描磁盘实用工具确认没有文件系统错误。 选择并按住 (或右键单击要扫描的驱动器) ，然后选择 " **属性**"。 选择 " **工具**"。 选择 " **立即检查** " 按钮。
-   确认硬盘上有足够的可用空间。 操作系统和某些应用程序需要足够的可用空间来创建交换文件和其他功能。 根据系统配置，具体要求会有所不同，但通常最好使用10% 到15% 的可用空间。

-   使用系统文件检查器工具修复丢失或损坏的系统文件。 系统文件检查器是 Windows 中的一个实用工具，它允许用户在 Windows 系统文件中扫描损坏并还原损坏的文件。 使用以下命令 ( # A0) 运行系统文件检查器工具。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅 [使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)。

-   **驱动程序验证程序**

    驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 如果发现驱动程序代码执行过程中出现错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，可在所有 Windows PC 上使用。 若要启动驱动程序验证程序管理器，请在命令提示下键入“验证程序”  。 你可以配置要验证的驱动程序。 验证驱动程序的代码在运行时会增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

过去，此停止代码的另一个可能原因是消耗了未分页的池内存。 如果非分页池内存完全耗尽，此错误可能会停止系统。 但是，在索引过程中，如果可用的非分页池内存量非常低，则另一个需要非分页池内存的内核模式驱动程序也会触发此错误。

 

