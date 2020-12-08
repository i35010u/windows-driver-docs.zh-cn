---
title: Bug 检查 0x18 REFERENCE_BY_POINTER
description: REFERENCE_BY_POINTER bug 检查的值为0x00000018。 这表明对象的引用计数对于对象的当前状态是非法的。
keywords:
- Bug 检查 0x18 REFERENCE_BY_POINTER
- REFERENCE_BY_POINTER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFERENCE_BY_POINTER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ee567aeec534631c12f46d34a4c85c153631a351
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815231"
---
# <a name="bug-check-0x18-reference_by_pointer"></a>Bug 检查0x18： \_ 通过 \_ 指针引用


\_通过 \_ 指针 BUG 检查引用的值为0x00000018。 这表明对象的引用计数对于对象的当前状态是非法的。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="reference_by_pointer-parameters"></a>\_通过 \_ 指针参数引用


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
<td align="left"><p>正在降低其引用计数的对象的对象类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在降低其引用计数的对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

对象的引用计数对于对象的当前状态是非法的。 每次驱动程序使用指向对象的指针时，驱动程序都会调用内核例程，以将对象的引用计数增加一。 当使用指针完成驱动程序时，驱动程序将调用另一个内核例程，以将引用计数减少1。

驱动程序必须与调用增加 (*引用*) 的例程匹配，并减少) 引用计数 (*取消* 引用。 此 bug 检查是由对象的引用计数不一致导致的。 通常情况下，不一致的原因是驱动程序将对象的引用计数减少了太多次，从而导致取消对对象的引用。 发生此 bug 检查的原因是，当对象的打开句柄仍为零时，对象的引用计数变为零。 如果对象的引用计数降到零以下，无论对象是否有打开句柄，也可能会发生这种情况。

<a name="resolution"></a>解决方法
----------

确保该驱动程序与对对象的引用计数增加和减少的例程的调用相匹配。 请确保您的驱动程序不会对取消引用对象的例程进行额外调用 (参见参数 2) 。

您可以使用调试器来帮助分析此问题。 有关详细信息，请参阅[使用 Windows 调试程序 (WinDbg) 进行故障转储分析](crash-dump-files.md)。 [**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

若要在对象上查找句柄和指针计数，请使用 **！ object** 调试器命令。

kd &gt; ！对象 *地址*

其中 *address* 是参数2中给定的对象的地址。

你还可以在代码中设置一个断点，使其导致此 stop 代码，并尝试单步执行出错的代码。

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

-   查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

 

 




