---
title: ndiskd.netreport
description: Ndiskd.netreport 扩展插件生成的整个网络堆栈的可视报表。
ms.assetid: 0FC134A8-8D91-4299-8D15-4E8EDD9ED855
keywords:
- ndiskd.netreport Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netreport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a072fcae39045e5183a096630b23185db5bed7b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363138"
---
# <a name="ndiskdnetreport"></a>!ndiskd.netreport


**！ Ndiskd.netreport**扩展插件可生成整个网络堆栈的可视报表。 报表 **！ ndiskd.netreport**生成的 HTML 文件，并且它将提供一个相关链接到其位置。 HTML 文件包含有关网络堆栈的详细的信息，因此如果您需要将其共享以进行分析可以通过电子邮件它而无需发送大型崩溃转储文件。

```console
!ndiskd.netreport [-outputpath <str>] [-jsononly] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-outputpath______"></span><span id="_______-OUTPUTPATH______"></span> *-outputpath*   
指定要写入报表文件的位置。

<span id="_______-jsononly______"></span><span id="_______-JSONONLY______"></span> *-jsononly*   
只会写入原始数据，任何 HTML。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.netreport**扩展要绘制的网络堆栈框关系图。

```console
1: kd> !ndiskd.netreport


NETWORK STACK REPORT


    Want more stuff?  Rerun with the -verbose flag
                                                                                            

    Report was saved to C:\Users\******\AppData\Local\Temp\NKDFE9F.html
    View the report                        Send in email
```

单击位于底部才能看到生成的报表的"查看报表"链接。 下图显示了从崩溃转储文件生成的最终报表。 每个垂直堆栈是细分为层显示堆栈的组件的网络适配器。 每个框的颜色生成的哈希组件，这意味着每次运行报表时，相同的组件将呈现具有相同颜色的名称。 这意味着可以轻松地找出特定驱动程序或适配器，如果你正在调试的问题。

![从故障转储的网络调试报告](images/!ndiskd-netreport-crashdump.png)

作为比较下, 图显示了从一种主动系统而不是崩溃转储文件生成的最终报表。 请注意，"显示数据的流"和"模拟的数据包，"HTML 页底部的两个更多选项，还有第四个选项卡顶部的"数据的流。"的报表 启用了出现因为调试对象机 NBL 跟踪这些选项，这样 **！ ndiskd.netreport**分析 NBL 跟踪日志，以直观地显示的信息。 如果未启用 NBL 跟踪，将不显示这些选项。 有关 NBL 跟踪的 NBL 日志的详细信息，请参阅[ **！ ndiskd.nbllog**](-ndiskd-nbllog.md)。

通过选中"显示数据的流"框中，您可以看到数据流动的位置的路径。 通过选中"模拟数据包"框中，您可以看到向上和向下数据移动数据流路径的动画的圆圈。 每个圆圈表示网络数据包。

![从活动的系统的网络调试报告](images/!ndiskd-netreport-activesystem.png)

从一种主动系统此第二个示例还显示从第一个示例，使用的崩溃转储文件的另一个差异。 第二个示例中的目标调试对象机之前预配内核调试通过网络，以便您可以看到具有数据流在堆栈上的网络适配器是 Microsoft 内核调试网络适配器。 除非已在调试对象上启用内核调试，通常隐藏此适配器。 实际上，内核调试网络适配器已保留的计算机的以太网适配器为调试会话，因此流量流动通过以太网。

可视化网络堆栈并看到流量流动的位置的功能可以用于快速确定的问题可能是。 这可以是虚拟交换机或服务器，具有更复杂的网络图前面的示例相比特别有用。 例如，在使用 NIC 组合的 Windows 服务器，可以看到多个网络堆栈跨其他流量负载平衡，并确定是否存在会影响另一个堆栈的一个堆栈的底部时出现问题。 若要查看有关调试报表来显示此网络的示例，请参阅[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)。 有关 NIC 组合的详细信息，请参阅[网络子系统性能使用 NIC 组合](https://docs.microsoft.com/previous-versions/dn567652(v=vs.85))。

**！ ndiskd.netreport**还有其他选项卡顶部的页上的系统、 摘要，以及数据流动 （如果适用）。 这些选项卡包含更多的网络堆栈的状态有关的有用信息。 下图显示了网络接口选项卡上，在摘要选项卡下。此选项卡中的表，可以在系统中查看有关的名称和标识符的网络接口的详细信息。

![网络调试报表网络接口](images/!ndiskd-netreport-activesystem-networkinterfaces.png)

数据的流选项卡上，如果在目标系统上启用了跟踪的 NBL 出现，显示了流量事件和有关每个详细信息的表。 下图显示前面所述在第二个示例调试报表中当前所用系统从数据的流选项卡。

![网络调试报表数据的流](images/!ndiskd-netreport-activesystem-dataflows.png)

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

[使用 NIC 组合的网络子系统性能](https://docs.microsoft.com/previous-versions/dn567652(v=vs.85))

 

 






