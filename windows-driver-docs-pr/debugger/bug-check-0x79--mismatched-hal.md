---
title: Bug 检查 0x79 MISMATCHED_HAL
description: "\"MISMATCHED_HAL bug 检查\" 的值为 \"0x00000079\"，表示 HAL 版本级别或配置与内核或计算机的配置不匹配。"
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
ms.openlocfilehash: 367a52541abb076111bf92461b94cff7fd7cfabf
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209311"
---
# <a name="bug-check-0x79-mismatched_hal"></a>Bug 检查0x79： HAL\_不匹配


不匹配的\_HAL bug 检查的值为0x00000079。 此错误检查表示硬件抽象层（HAL）修订级别或配置与内核或计算机的配置不匹配。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="mismatched_hal-parameters"></a>不匹配的\_HAL 参数


参数1指示不匹配的类型。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">导致.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Ntoskrnl.exe 的主要处理器控制块（PRCB）级别。</p></td>
<td align="left"><p>Hal 的主要 PRCB 级别。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>PRCB 版本不匹配。 （某些内容已过期。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>Ntoskrnl.exe 的生成类型。</p></td>
<td align="left"><p>Hal 的生成类型。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>生成类型不匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>加载器参数扩展的大小。</p></td>
<td align="left"><p>加载器参数扩展的主版本。</p></td>
<td align="left"><p>加载器参数扩展的次版本。</p></td>
<td align="left"><p>加载器（ntldr）和 HAL 版本不匹配。</p></td>
</tr>
</tbody>
</table>

 

当参数1等于0x2 时，将使用以下生成类型代码：

-   0：启用多处理器的免费生成

-   1：启用多处理器的已检查生成

-   2：单处理器免费生成

-   3：单处理器检查生成

<a name="cause"></a>原因
-----

当用户手动更新 Ntoskrnl.exe 或 Hal 时，通常会发生不匹配的\_HAL bug 检查。

此错误还可能指示这两个文件中的一个已过期。 否则，计算机可能会错误地安装多处理器 HAL 和单处理器内核，反之亦然。

Ntoskrnl.exe 内核文件适用于单处理器系统，Ntkrnlmp 适用于多处理器系统。 但是，这些文件名与安装媒体上的文件相对应。安装了 Windows 操作系统后，无论使用何种源文件，都将该文件重命名为 Ntoskrnl.exe。 HAL 文件在安装后也使用名称 Hal，但在较旧版本的 Windows 上，安装媒体上有几个可能的 HAL 文件。

<a name="resolution"></a>分辨率
----------

使用产品 CD 或 Windows 安装程序磁盘重新启动计算机。 在欢迎屏幕上，按 F10 启动恢复控制台。 使用 "**复制**" 命令将正确的 HAL 或内核文件从原始 CD 复制到硬盘上的相应文件夹中。 **Copy**命令检测你要复制的文件是否为 Microsoft 压缩文件格式。 如果是这样，它会自动扩展在目标驱动器上复制的文件。

 

 




