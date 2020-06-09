---
title: ndiskd.netreport
description: Ndiskd. netreport 扩展会生成整个网络堆栈的可视报表。
ms.assetid: 0FC134A8-8D91-4299-8D15-4E8EDD9ED855
keywords:
- ndiskd netreport Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netreport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 68c74aca795441d1715ab965fd65527f98a4d1ee
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534728"
---
# <a name="ndiskdnetreport"></a>!ndiskd.netreport


**！ Ndiskd netreport**扩展生成整个网络堆栈的视觉报表。 报表 **！ ndiskd**将生成一个 HTML 文件，它将为你显示指向其位置的链接。 该 HTML 文件包含有关网络堆栈的详细信息，因此，如果需要共享它进行分析，可以通过电子邮件发送该文件，而无需发送大型故障转储文件。

```console
!ndiskd.netreport [-outputpath <str>] [-jsononly] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-outputpath______"></span><span id="_______-OUTPUTPATH______"></span>*-outputpath*   
指定报表文件的写入位置。

<span id="_______-jsononly______"></span><span id="_______-JSONONLY______"></span>*-jsononly*   
仅写入原始数据，没有 HTML。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

运行 **！ ndiskd. netreport**扩展以绘制网络堆栈的方框关系图。

```console
1: kd> !ndiskd.netreport


NETWORK STACK REPORT


    Want more stuff?  Rerun with the -verbose flag
                                                                                            

    Report was saved to C:\Users\******\AppData\Local\Temp\NKDFE9F.html
    View the report                        Send in email
```

单击底部的 "查看报表" 链接可查看生成的报表。 下图显示了从故障转储文件生成的网络报表。 每个垂直堆栈都是一个网络适配器，分为显示堆栈组件的层。 每个框的颜色通过对组件名称进行哈希处理，这意味着每次运行报表时，相同的组件都将以相同的颜色呈现。 这意味着，如果您正在调试某个特定的驱动程序或适配器，就可以轻松地选择它。

![故障转储中的网络调试报告](images/!ndiskd-netreport-crashdump.png)

作为比较，下图显示了从活动系统而不是故障转储文件生成的网络报表。 请注意，在 HTML 页的底部有另外两个选项显示 "显示数据流" 和 "模拟数据包"，并且在报表顶部有一个 "数据流" 的第四个选项卡。 出现这些选项是因为调试对象计算机启用了 NBL 跟踪，这允许 **！ ndiskd**分析 NBL 跟踪日志以直观地显示信息。 如果未打开 NBL 跟踪，则不会显示这些选项。 有关 NBL 跟踪和 NBL 日志的详细信息，请参阅[**！ ndiskd. nbllog**](-ndiskd-nbllog.md)。

通过选中 "显示数据流" 框，可以看到数据流动的路径。 通过选中 "模拟包" 框，您可以看到在数据流路径中上下移动的动画圆圈。 每个圆圈表示一个网络数据包。

![来自活动系统的网络调试报告](images/!ndiskd-netreport-activesystem.png)

此第二个示例来自活动系统，另外还显示了第一个示例中使用故障转储文件的另一个不同之处。 第二个示例中的目标调试对象计算机已设置为通过网络进行内核调试，因此你可以在堆栈上看到网络适配器，数据流是 Microsoft 内核调试网络适配器。 除非在调试对象计算机上启用了内核调试，否则此适配器通常处于隐藏状态。 事实上，内核调试网络适配器已经为调试会话保留了计算机的以太网适配器，因此流量通过以太网流动。

能够直观显示网络堆栈并查看流量的流动位置，可以快速确定问题所在的位置。 这对于虚拟交换机或服务器特别有用，其网络图比前面的示例更复杂。 例如，在使用 NIC 组合的 Windows Server 上，你可以查看多个网络堆栈是否相互交叉以平衡流量负载，并确定某个堆栈底部是否存在影响另一堆栈的问题。 若要查看显示此的网络调试报表的示例，请参阅[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)。 有关 NIC 组合的详细信息，请参阅[对网络子系统性能使用 NIC 组合](https://docs.microsoft.com/previous-versions/dn567652(v=vs.85))。

**！ ndiskd**在页面顶部还有其他选项卡，用于系统、摘要和数据流（如果适用）。 这些选项卡包含有关网络堆栈状态的更多有用信息。 下图显示了 "摘要" 选项卡下的 "网络接口" 选项卡。此选项卡中的表使你可以查看有关系统中网络接口的名称和标识符的详细信息。

![网络调试报表网络接口](images/!ndiskd-netreport-activesystem-networkinterfaces.png)

"数据流" 选项卡，如果在目标系统上启用了 NBL 跟踪，则会显示一个流量表，其中显示了有关每个事件的详细信息。 下图显示了前面所述的第二个示例 "调试" 报表中的活动系统的 "数据流" 选项卡。

![网络调试报表数据流](images/!ndiskd-netreport-activesystem-dataflows.png)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.nbllog**](-ndiskd-nbllog.md)

[对网络子系统性能使用 NIC 组合](https://docs.microsoft.com/previous-versions/dn567652(v=vs.85))

 

 






