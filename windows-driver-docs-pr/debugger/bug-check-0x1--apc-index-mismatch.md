---
title: Bug 检查 0x1 APC_INDEX_MISMATCH
description: 0x00000001。
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
ms.openlocfilehash: dabfde020fde2de1d4ec64fe002011876feda59f
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492532"
---
# <a name="bug-check-0x1-apcindexmismatch"></a>Bug 检查 0x1：APC\_INDEX\_MISMATCH


APC\_索引\_不匹配错误检查的值为 0x00000001。 这指示 APC （异步过程调用） 状态索引中已存在不匹配。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="apcindexmismatch-parameters"></a>APC\_索引\_不匹配参数


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
<td align="left"><p>系统函数 （系统调用） 或辅助角色例程的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left">当前线程的值<strong>ApcStateIndex</strong>字段。</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>当前线程的 CombinedApcDisable 字段的值。 此字段包含两个单独的 16 位字段：(<em>线程</em>-&gt;<strong>SpecialApcDisable</strong> &lt; &lt; 16) |<em>线程</em>-&gt;<strong>KernelApcDisable</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>调用类型 （0-系统调用，1-辅助角色例程）。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cause"></a>原因
-----

此 bug 检查的最常见原因是当文件系统或驱动程序具有不匹配的调用，以禁用再重新启用 Apc 序列。 关键数据项*线程*-&gt;**CombinedApcDisable**字段。 **CombinedApcDisable**字段包含两个单独的 16 位字段：**SpecialApcDisable**并**KernelApcDisable**。 其中一个字段的负值指示，禁用驱动程序具有特殊或正常 Apc （分别） 而无需重新启用它们。 正值指示驱动程序，已启用特殊或正常 Apc 次数过多。

## <a name="resolution"></a>分辨率
----------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

可以使用[ **！ apc** ](-apc.md)扩展显示的内容的一个或多个异步过程调用 (Apc)。

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

有关详细信息，请参阅以下主题：

[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

## <a name="remarks"></a>备注
-------

这是内核内部错误。 从系统调用 exit 出现此错误。 检查此错误的可能原因是当文件系统或驱动程序具有不匹配的序列的系统调用进入或离开受保护或关键区域。 例如，每次调用[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)必须匹配调用[ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)。 如果你正在开发一个驱动程序，则可以使用[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)，静态分析工具，可在 Windows 驱动程序工具包中，若要在代码中检测问题，然后再交付您的驱动程序。 运行与的 Static Driver Verifier [CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)规则以验证你的源代码，使用这些系统调用正确的顺序。

 

 




