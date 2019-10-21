---
title: Bug 检查 0x1 APC_INDEX_MISMATCH
description: 0x00000001.
ms.assetid: 01e64516-809c-49ce-9aaa-b4e439ac575b
keywords:
- Bug 检查 0x1 APC_INDEX_MISMATCH
- APC_INDEX_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- APC_INDEX_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50b3471b83fe57ae6d99c4a3fcf649807e80754f
ms.sourcegitcommit: 6d7f25f280af5fd4f4d9337d131c2a22288847fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359584"
---
# <a name="bug-check-0x1-apc_index_mismatch"></a>Bug 检查0x1： APC \_INDEX \_MISMATCH

APC \_INDEX \_MISMATCH bug 检查的值为0x00000001。 这表示异步过程调用（APC）状态索引中存在不匹配的情况。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="apc_index_mismatch-parameters"></a>APC \_INDEX \_MISMATCH 参数

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
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
<td align="left"><p>系统函数（系统调用）或辅助例程的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left">当前线程的<strong>ApcStateIndex</strong>字段的值。</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>当前线程的<strong>CombinedApcDisable</strong>字段的值。 此字段由两个单独的16位字段组成：（<em>Thread</em> &gt;<strong>SpecialApcDisable</strong> &lt; &lt; 16） |<strong>KernelApcDisable</strong><em>线程</em>&gt;。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>调用类型：</p><ul><li>0-系统调用</li><li>1-辅助例程</li></ul></p></td>
</tr>
</tbody>
</table>

 
<a name="cause"></a>原因
-----

此错误检查的最常见原因是文件系统或驱动程序的调用序列不匹配，无法禁用和重新启用 Apc。 Key data 项是*线程*&gt;**CombinedApcDisable**字段。 **CombinedApcDisable**字段包含两个单独的16位字段： **SpecialApcDisable**和**KernelApcDisable**。 任何一个字段的负值都表明驱动程序已禁用特殊或普通 Apc （分别）而不重新启用它们。 正值表示驱动程序已启用特殊或普通 Apc 的次数过多。


<a name="resolution"></a>分辨率
----------

### <a name="debugging-with-windbg"></a>用 WinDbg 进行调试

[ **！分析**](-analyze.md)调试器扩展显示有关 bug 检查的信息，可帮助确定根本原因。

您可以使用[ **！ apc**](-apc.md)扩展显示一个或多个异步过程调用（apc）的内容。

你还可以在代码中设置一个断点，该断点位于此 stop 代码之前，并尝试单步执行错误代码。

有关使用 WinDbg 的详细信息，请参阅[使用 Windows 调试器（WinDbg）进行故障转储分析](crash-dump-files.md)。


### <a name="debugging-without-windbg"></a>不带 WinDbg 的调试

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

-   查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

有关其他常规疑难解答信息，请参阅[蓝屏数据](blue-screen-data.md)。


<a name="remarks"></a>备注
-------

此 bug 检查是内核中的内部错误的结果。 退出系统调用时出现此错误。 此错误检查的可能原因是文件系统或驱动程序的系统调用序列不匹配，无法进入或离开受保护的或关键区域。 例如，每次调用[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)时，都必须具有对[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)的匹配调用。 

如果要开发驱动程序，可以使用 Windows 驱动程序工具包中提供的静态[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)器（一种静态分析工具）来检测你的代码中的问题，然后再交付驱动程序。 使用[CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)规则运行静态驱动程序验证程序，以验证你的源代码是否按正确的顺序使用了这些系统调用。

