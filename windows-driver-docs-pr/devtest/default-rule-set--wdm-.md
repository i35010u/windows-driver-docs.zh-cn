---
title: 默认规则集 (WDM)
description: 默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。
ms.assetid: F03BEEDE-ED6E-4202-9FF5-74A098702E12
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8596f2fcac51dfbdd424b97fd9864b027a6468a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385059"
---
# <a name="default-rule-set-wdm"></a>默认规则集 (WDM)


默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。

[ (WDM) ](ddi-usage-rule-set--wdm-.md) 
 的 DDI 使用情况规则集[ (WDM) ](irpprocessing-rule-set--wdm-.md) 
 的 IrpProcessing 规则集[ (WDM) ](irptracking-rule-set--wdm-.md) 
 的 IrpTracking 规则集在[WDM) ](irql-rule-set--wdm-.md) 
 (Irql 规则集[ (WDM) ](localirpprocessing-rule-set--wdm-.md) 
 的 LocalIrpProcessing 规则集[ (WDM) ](locking-rule-set--wdm-.md) 
 锁定规则集[杂项规则集 (WDM) ](miscellaneous-rule-set--wdm-.md) 
[ (WDM) ](irppending-rule-set--wdm-.md) 
 的 IrpPending 规则集**选择默认规则**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **默认**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

