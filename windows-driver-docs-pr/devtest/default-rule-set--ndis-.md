---
title: 默认规则集 (NDIS)
description: 默认规则集 (Default.sdv) 指定建议的规则分析您的驱动程序时要使用的集。
ms.assetid: ED809122-5938-4087-AAB8-0D3EB6DB1092
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 40ad2406e83bc1b02a7c74235f141acb9a060429
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341137"
---
# <a name="default-rule-set-ndis"></a>默认规则集 (NDIS)


默认规则集 (Default.sdv) 指定建议的规则分析您的驱动程序时要使用的集。

[DDI 使用规则集 (NDIS)](ddi-usage-rule-set--ndis-.md)
[IRQL 规则集 (NDIS)](irql-rule-set--ndis-.md)
[锁定规则集 (NDIS)](locking-rule-set--ndis-.md)
[内存使用率规则设置 (NDIS)](memory-usage-rule-set--ndis-.md)
[杂项规则集 (NDIS)](miscellaneous-rule-set--ndis-.md)
[OidProcessing 规则集 (NDIS)](oidprocessing-rule-set--ndis-.md)
**若要选择的默认规则**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**默认**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Default.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





