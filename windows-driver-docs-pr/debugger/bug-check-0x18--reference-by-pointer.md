---
title: Bug 检查从 0x18 REFERENCE_BY_POINTER
description: REFERENCE_BY_POINTER bug 检查具有 0x00000018 值。 这指示一个对象的引用计数是非法的对象的当前状态。
ms.assetid: 911fa821-5e59-4f20-a31b-148064e6c113
keywords:
- Bug 检查从 0x18 REFERENCE_BY_POINTER
- REFERENCE_BY_POINTER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFERENCE_BY_POINTER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a039ce590c9b522ab419adf119c60afb587b1846
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902287"
---
# <a name="bug-check-0x18-referencebypointer"></a>Bug 检查 0x18：引用\_BY\_指针


引用\_BY\_指针错误检查的值为 0x00000018。 这指示一个对象的引用计数是非法的对象的当前状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="referencebypointer-parameters"></a>引用\_BY\_指针参数


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
<td align="left"><p>要降低其引用计数对象的对象类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>要降低其引用计数的对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

一个对象的引用计数是非法的对象的当前状态。 驱动程序使用一个指针指向一个对象，每次该驱动程序调用内核例程，以增加一对象的引用计数。 当驱动程序通过指针时，该驱动程序调用另一个内核例程的引用计数减少 1。

驱动程序必须与匹配对增加的例程的调用 (*引用*) 和减少 (*取消引用*) 的引用计数。 此 bug 检查是由对象的引用计数不一致引起的。 通常情况下，不一致引起的驱动程序，减少引用计数对象的次数过多，进行取消引用该对象的额外调用。 由于对象的引用计数变为零仍打开的句柄到对象时，可能出现此 bug 检查。 也可能发生时对象的引用计数降至低于零，指示有打开的句柄到对象。

<a name="resolution"></a>分辨率
----------

请确保该驱动程序匹配的增加和减少的对象的引用计数的例程的调用。 请确保您的驱动程序不会进行取消引用该对象的例程的额外调用 （请参阅参数 2）。

可以使用调试器来帮助分析此问题。 有关详细信息，请参阅[使用 Windows 调试程序 (WinDbg) 进行故障转储分析](crash-dump-files.md)。 [ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

若要查找的句柄和指针计数对象上，使用 **！ 对象**调试器命令。

kd&gt; !object *address*

其中*地址*是参数 2 中提供的对象的地址。

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

 

 




