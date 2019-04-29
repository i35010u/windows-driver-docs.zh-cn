---
title: Bug 检查 0x79 MISMATCHED_HAL
description: MISMATCHED_HAL bug 检查具有 0x00000079，该值指示，HAL 修订级别或配置不匹配的内核或此计算机的值。
ms.assetid: 2d063c2a-c647-4436-b005-04f71a4d2b66
keywords:
- Bug 检查 0x79 MISMATCHED_HAL
- MISMATCHED_HAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MISMATCHED_HAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3b423ca79fe75656a3839868e6e7fc95bbe9f3c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367345"
---
# <a name="bug-check-0x79-mismatchedhal"></a>Bug 检查 0x79：不匹配的\_HAL


不匹配\_HAL bug 检查的值为 0x00000079。 此 bug 检查指示，硬件抽象层 (HAL) 的修订级别或配置不匹配的内核或计算机。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="mismatchedhal-parameters"></a>不匹配的\_HAL 参数


参数 1 指示不匹配的类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Ntoskrnl.exe 主要处理器控制块 (PRCB) 级别。</p></td>
<td align="left"><p>Hal.dll 主要 PRCB 级别。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>PRCB 版本级别不匹配。 （某些已过时。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>Ntoskrnl.exe 生成类型。</p></td>
<td align="left"><p>Hal.dll 生成类型。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>生成类型不匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>加载程序参数扩展的大小。</p></td>
<td align="left"><p>加载程序参数扩展的主要版本。</p></td>
<td align="left"><p>加载程序参数扩展次要版本。</p></td>
<td align="left"><p>加载器 (ntldr) 和 HAL 版本不匹配。</p></td>
</tr>
</tbody>
</table>

 

如果参数 1 等于 0x2，使用以下生成类型代码：

-   0:多个处理器的免费生成

-   1：多个处理器的已检验的版本

-   2：单处理器免费生成

-   3：单处理器已检验的版本

<a name="cause"></a>原因
-----

不匹配\_HAL bug 检查情况通常发生在用户手动更新 Ntoskrnl.exe 或 Hal.dll。

错误也可能表示这两个文件之一已过时。 或者计算机可能会错误地多处理器 HAL 和安装，是单处理器内核，反之亦然。

Ntoskrnl.exe 内核文件适用于单处理器系统并 Ntkrnlmp.exe 是对于多处理器系统。 但是，这些文件的名称对应于安装介质上的文件。安装 Windows 操作系统后，该文件重命名为 Ntoskrnl.exe，而不考虑使用的源文件。 HAL 文件还安装完成后，使用 Hal.dll 的名称，但有几个可能的 HAL 文件安装媒体上。 有关详细信息，请参阅"安装检查生成"Windows Driver Kit (WDK) 中。

<a name="resolution"></a>分辨率
----------

通过使用产品光盘或 Windows 安装盘重新启动计算机。 在欢迎屏幕上，按 F10 即可启动故障恢复控制台。 使用**复制**命令以将正确的 HAL 或内核文件从原始 CD 复制到硬盘上的相应文件夹。 **复制**命令检测到要复制的文件是否为 Microsoft 压缩的文件格式。 如果是这样，它将自动展开复制目标驱动器的文件。

 

 




