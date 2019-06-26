---
title: 解释静态驱动程序验证程序结果
description: 解释静态驱动程序验证程序结果
ms.assetid: ec7e3b90-5d55-411a-8cfe-a1c9c4029694
keywords:
- 静态驱动程序验证程序 WDK，显示选项
- StaticDV WDK 显示选项
- SDV WDK 显示选项
- 静态驱动程序验证程序 WDK，验证结果
- StaticDV WDK，验证结果
- SDV WDK，验证结果
- 验证结果 WDK Static Driver Verifier
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: f85f9192aefb7d79f4eed1a29923d4a7a37685bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373703"
---
# <a name="interpreting-static-driver-verifier-results"></a>解释静态驱动程序验证程序结果


当启动 Static Driver Verifier 从 Visual Studio 并运行您的驱动程序的分析，结果将显示在**结果**摘要 Main 选项卡上。

![显示结果后运行的 static driver verifier 摘要的屏幕截图。](images/sdv-results-vs.png)

### <a name="span-idstatisticsspanspan-idstatisticsspanspan-idstatisticsspanstatistics"></a><span id="Statistics"></span><span id="statistics"></span><span id="STATISTICS"></span>统计信息

**入口点**报告在驱动程序源代码中找到的入口点的数目。 入口点是驱动程序所提供的回调或调度例程。 定义使用函数角色类型声明的入口点。 若要执行的分析，SDV 必须 fiind 至少一个入口点。 有关详细信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

**发现的缺陷**报告在分析期间发现的缺陷数。 缺陷是 DDI 符合性规则的冲突。

**执行的测试**报告在分析过程中测试的规则数。 这些是在选择的规则**规则**选项卡。

### <a name="span-idstatusspanspan-idstatusspanspan-idstatusspanstatus"></a><span id="Status"></span><span id="status"></span><span id="STATUS"></span>状态

报告分析的状态。 完成后，可以查看找到的结果。

### <a name="span-idresultsspanspan-idresultsspanspan-idresultsspanresults"></a><span id="Results"></span><span id="results"></span><span id="RESULTS"></span>结果

<span id="Completed__Rule_"></span><span id="completed__rule_"></span><span id="COMPLETED__RULE_"></span>**已完成 （规则）**  
SDV 测试规则的冲突的驱动程序，但它可能不会证明规则的任何冲突。

此结果并不意味着该驱动程序是免费的错误。 这仅意味着 SDV 可以证明它违反了验证阶段中的规则。

<span id="Defect"></span><span id="defect"></span><span id="DEFECT"></span>**缺陷**  
如果 SDV 报告一个或多个缺陷，请单击**缺陷**链接到[使用静态的驱动程序验证工具报告](using-the-static-driver-verifier-report.md)查看错误的跟踪。

<span id="Not_Applicable"></span><span id="not_applicable"></span><span id="NOT_APPLICABLE"></span>**不适用**  
SDV 测试规则的冲突的驱动程序，但该驱动程序不支持的入口点所需的分析或驱动程序未调用的函数的规则监视。

如果该规则监视函数调用 （通常情况下，对资源的指针） 中某个特定参数和驱动程序不会调用该函数，或者未引用该参数，此规则不适用于驱动程序。

如果该驱动程序未指定入口点，并且它调用的函数，规则监视器，此结果可能指示 SDV 找不到或未正确解释的入口点。 若要确认这种情况发生，检查，并如有必要，更正[Sdv map.h](sdv-map-h.md)文件。 有关此过程的信息，请参阅[扫描该驱动程序](scanning-the-driver.md)。

有关每个规则的详细信息，请参阅[驱动程序验证程序的静态规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)引用。

若要查看更多的驱动程序，运行验证使用不同的规则。

<span id="Timeouts"></span><span id="timeouts"></span><span id="TIMEOUTS"></span>**超时**  
SDV 停止验证规则，因为它超出了其用于验证每个规则的时间限制。 设置时间限制[静态驱动程序验证工具选项文件](static-driver-verifier-options-file.md)，或在最大时间字段中**配置**选项卡。

超时值被视为无结论的结果。 它不指示驱动程序错误。 如果 SDV 报告超时，扩展验证所允许的时间 ( **SDV\_SlamConfig\_超时**sdv default.xmlfile 中的值) 并再次运行验证。

<span id="Completed__Property_"></span><span id="completed__property_"></span><span id="COMPLETED__PROPERTY_"></span>**已完成 （属性）**  
SDV 已运行指定的驱动程序的驱动程序属性规则。 驱动程序属性规则检查驱动程序功能或支持的功能，以做进一步分析的准备。 例如，驱动程序属性规则， **CancelRoutine**，检查是否已注册的 WDM 驱动程序[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程。 如果*取消*例程未检测到，不适用于特定 WDM 规则。 这意味着未满足的驱动程序属性。

<span id="Satisfied__Property_"></span><span id="satisfied__property_"></span><span id="SATISFIED__PROPERTY_"></span>**满足 （属性）**  
SDV 已运行指定的驱动程序的驱动程序属性规则。 驱动程序属性规则检查驱动程序功能或支持的功能，以做进一步分析的准备。 例如，驱动程序属性规则， **CancelRoutine**，检查是否已注册的 WDM 驱动程序[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程。 如果*取消*例程进行检测，则应用特定 WDM 规则。 这意味着已满足驱动程序属性

<span id="Spaceouts"></span><span id="spaceouts"></span><span id="SPACEOUTS"></span>**Spaceouts**  
SDV 停止验证，因为它超出了验证规则的内存限制的规则数。 在中设置的内存限制[静态驱动程序验证工具选项文件](static-driver-verifier-options-file.md)，sdv default.xml。

Spaceout 被视为无结论的结果。 如果 SDV 报告 spaceout，扩展用于验证分配的空间 ( **SDV\_SlamConfig\_Spaceout** sdv default.xml 文件中的值) 并再次运行验证。

<span id="Other"></span><span id="other"></span><span id="OTHER"></span>**其他**  

SDV 遇到内部错误从中它无法恢复的次数。  请参阅[静态 Driver Verifier 错误消息](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-error-messages)有关错误的详细信息页上和调试。

 

 





