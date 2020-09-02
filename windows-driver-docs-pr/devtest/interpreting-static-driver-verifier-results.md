---
title: 解释静态驱动程序验证程序结果
description: 解释静态驱动程序验证程序结果
ms.assetid: ec7e3b90-5d55-411a-8cfe-a1c9c4029694
keywords:
- 静态驱动程序验证程序 WDK，显示选项
- StaticDV WDK，显示选项
- SDV WDK，显示选项
- 静态驱动程序验证程序 WDK，验证结果
- StaticDV WDK，验证结果
- SDV WDK，验证结果
- 验证结果 WDK 静态驱动程序验证程序
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 00d587dcf11aa8d96bc3c96c083234b5ca95a3bd
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383001"
---
# <a name="interpreting-static-driver-verifier-results"></a>解释静态驱动程序验证程序结果


当你从 Visual Studio 中启动静态驱动程序验证程序并运行对你的驱动程序的分析时，结果将显示在 "主" 选项卡上的 " **结果** 摘要" 中。

![显示运行静态驱动程序验证程序后的结果摘要的屏幕截图。](images/sdv-results-vs.png)

### <a name="span-idstatisticsspanspan-idstatisticsspanspan-idstatisticsspanstatistics"></a><span id="Statistics"></span><span id="statistics"></span><span id="STATISTICS"></span>标识

**S** 报告驱动程序源代码中的入口点的数量。 入口点是驱动程序提供的回调或调度例程。 使用函数角色类型声明定义入口点。 若要执行分析，SDV 必须 fiind 至少一个入口点。 有关详细信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。

**发现的缺陷** 报告在分析期间发现的缺陷数。 缺陷是违反 DDI 合规性规则的问题。

**执行的测试** 报告在分析过程中测试的规则数。 这些是你在 " **规则** " 选项卡上选择的规则。

### <a name="span-idstatusspanspan-idstatusspanspan-idstatusspanstatus"></a><span id="Status"></span><span id="status"></span><span id="STATUS"></span>状态值

报告分析的状态。 完成后，您可以查看找到的结果。

### <a name="span-idresultsspanspan-idresultsspanspan-idresultsspanresults"></a><span id="Results"></span><span id="results"></span><span id="RESULTS"></span>后果

<span id="Completed__Rule_"></span><span id="completed__rule_"></span><span id="COMPLETED__RULE_"></span>**已完成 (规则) **  
SDV 测试了驱动程序是否违反了规则，但无法证明规则的任何冲突。

此结果并不意味着该驱动程序是免费的。 这意味着，SDV 无法证明它违反了验证过程中的规则。

<span id="Defect"></span><span id="defect"></span><span id="DEFECT"></span>**故障**  
如果 SDV 报告了一个或多个缺陷，则单击 " **缺陷** " 链接以 [使用 "静态驱动程序验证程序" 报告](using-the-static-driver-verifier-report.md) 查看错误的跟踪。

<span id="Not_Applicable"></span><span id="not_applicable"></span><span id="NOT_APPLICABLE"></span>**不适用**  
SDV 测试了驱动程序是否违反了规则，但驱动程序不支持分析所需的入口点，或者驱动程序未调用规则所监视的函数。

如果规则监视函数调用中的特定参数 (通常情况下，指向资源的指针) 并且驱动程序未引用该函数，或者未引用该参数，则该规则不适用于该驱动程序。

如果驱动程序指定了入口点并且它调用了规则所监视的函数，则此结果可能表示 SDV 找不到或未正确解释入口点。 若要确认出现此情况，请检查并根据需要更正 [Sdv](sdv-map-h.md) 文件。 有关此过程的信息，请参阅 [扫描驱动程序](scanning-the-driver.md)。

有关每个规则的详细信息，请参阅 [静态驱动程序验证程序规则](/windows-hardware/drivers/ddi/index) 参考。

若要进一步检查驱动程序，请使用不同的规则运行验证。

<span id="Timeouts"></span><span id="timeouts"></span><span id="TIMEOUTS"></span>**超**  
SDV 已停止验证规则，因为它超过了验证每个规则的时间限制。 时间限制在 [静态驱动程序验证程序选项文件](static-driver-verifier-options-file.md)中设置，或在 " **配置** " 选项卡上的 "最大时间" 字段中设置。

超时被视为无结论结果。 它不指示驱动程序错误。 如果 SDV 报告超时，请在 sdv-default.xml文件) 中将验证允许的时间延长 (" **SDV \_ SlamConfig \_ timeout** " 值，然后再次运行验证。

<span id="Completed__Property_"></span><span id="completed__property_"></span><span id="COMPLETED__PROPERTY_"></span>**已完成 (属性) **  
SDV 为指定的驱动程序运行了驱动程序属性规则。 驱动程序属性规则检查驱动程序功能或支持的功能，并是 prelude 进行进一步分析。 例如，驱动程序属性规则 **CancelRoutine**检查 WDM 驱动程序是否注册了 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程。 如果未检测到 *取消* 例程，则不会应用特定的 WDM 规则。 这意味着未满足驱动程序属性的要求。

<span id="Satisfied__Property_"></span><span id="satisfied__property_"></span><span id="SATISFIED__PROPERTY_"></span>**满足 (属性) **  
SDV 为指定的驱动程序运行了驱动程序属性规则。 驱动程序属性规则检查驱动程序功能或支持的功能，并是 prelude 进行进一步分析。 例如，驱动程序属性规则 **CancelRoutine**检查 WDM 驱动程序是否注册了 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程。 如果检测到 *取消* 例程，则应用特定的 WDM 规则。 这意味着已满足驱动程序属性

<span id="Spaceouts"></span><span id="spaceouts"></span><span id="SPACEOUTS"></span>**Spaceouts**  
SDV 停止验证的规则数，因为它超过了用于验证该规则的内存限制。 内存限制在 [静态驱动程序验证程序选项文件](static-driver-verifier-options-file.md)中设置 sdv-default.xml。

Spaceout 被视为无结论结果。 如果 SDV 报告 spaceout，请将为验证分配的空间扩展 (sdv-default.xml 文件中的 **SDV \_ SlamConfig \_ spaceout** 值) ，然后再次运行验证。

<span id="Other"></span><span id="other"></span><span id="OTHER"></span>**以外**  

SDV 遇到无法从中恢复的内部错误的次数。  有关错误和调试的详细信息，请参阅 [静态驱动程序验证程序错误消息](./static-driver-verifier-error-messages.md) 页面。

 

