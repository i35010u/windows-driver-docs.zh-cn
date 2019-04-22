---
title: Bug Check 0x24 NTFS_FILE_SYSTEM
description: NTFS_FILE_SYSTEM bug 检查具有 0x00000024 值。 这表示 ntfs.sys，使系统能够读取和写入到 NTFS 驱动器的驱动程序文件中出现问题。
ms.assetid: 9d2dd8a8-b550-4392-b663-6902a015ef7b
keywords:
- Bug Check 0x24 NTFS_FILE_SYSTEM
- NTFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NTFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ac890eb3864ddf25bd0a6823c077442f9cc4183f
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238638"
---
# <a name="bug-check-0x24-ntfsfilesystem"></a>Bug 检查 0x24：NTFS\_FILE\_SYSTEM


NTFS\_文件\_检查系统错误的值为 0x00000024。 这表示 ntfs.sys，使系统能够读取和写入到 NTFS 驱动器的驱动程序文件中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="ntfsfilesystem-parameters"></a>NTFS\_文件\_系统参数


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
<td align="left"><p>指定源代码文件和行号信息。 高 16 位 （"0x"后的前四个十六进制数字） 标识由其标识符编号的源代码文件。 低 16 位标识发生错误检查的文件中的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果<strong>NtfsExceptionFilter</strong>是在堆栈上，此参数指定的地址的异常记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>如果<strong>NtfsExceptionFilter</strong>是在堆栈上，此参数指定的上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查的一个可能的原因是磁盘损坏。 NTFS 文件系统或在硬盘上的坏扇区 （扇区） 中的损坏可导致此错误。 损坏的硬盘驱动器 (SATA/IDE) 驱动程序可能会反过来影响系统的能够读取和写入到磁盘，从而导致错误。

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令参数 3 中，并使用[ **kb （显示堆栈回溯）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**若要解决磁盘损坏问题：**

-   事件查看器检查系统日志，可帮助找出设备或导致错误的驱动程序中出现的硬盘驱动器与相关的错误消息。

-   请尝试禁用任何病毒扫描程序、 备份程序或持续监视系统的磁盘碎片整理程序工具。

-   您还应运行硬件诊断与存储子系统相关的系统制造商提供。

-   使用扫描磁盘实用程序以确认没有任何文件系统错误。 右键单击你想要扫描，并选择在驱动器上**属性**。 单击**工具**。 单击**立即检查**按钮。
-   确认在硬盘上没有足够的可用空间。 操作系统和某些应用程序需要足够的可用空间来创建交换文件和其他功能。 根据系统配置，具体要求各不相同，但它通常是最好有可用的 10%到 15%可用空间。

-   使用系统文件检查器工具来修复丢失或损坏系统文件。 系统文件检查器是一个实用程序允许用户在 Windows 系统文件损坏扫描和还原 Windows 中的损坏的文件。 使用以下命令运行系统文件检查器 (SFC.exe)。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅[使用的系统文件检查器工具来修复丢失或损坏系统文件](https://support.microsoft.com/kb/929833)。

-   **驱动程序验证程序**

    驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 如果它看到错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。

在过去，此停止代码的另一个可能原因是非分页缓冲的池内存耗尽。 如果完全耗尽的非分页缓冲的池内存，则此错误可以停止系统。 但是，在索引过程中，如果可用的非分页缓冲的池内存量为非常低，需要非分页缓冲的池内存的另一个内核模式驱动程序还可以触发此错误。

 

 




