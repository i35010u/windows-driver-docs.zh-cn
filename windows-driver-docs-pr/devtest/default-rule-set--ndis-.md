---
title: 默认规则集 (NDIS)
description: 了解 (NDIS) 的默认规则集，它指定了在分析驱动程序时要使用的建议规则集。
ms.assetid: ED809122-5938-4087-AAB8-0D3EB6DB1092
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 093dd4a7ae25a9bc0cda6bed8c9c3f581c3ff490
ms.sourcegitcommit: cccf9ba62af357aad1016addbbf6c42c7f564412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2020
ms.locfileid: "91606493"
---
# <a name="default-rule-set-ndis"></a>默认规则集 (NDIS)


默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。

[NDIS 使用情况规则集 (NDIS) ](ddi-usage-rule-set--ndis-.md) 
[IRQL 规则集 (NDIS) ](irql-rule-set--ndis-.md) 
[ (NDIS) ](locking-rule-set--ndis-.md) 
 锁定规则集[内存使用率规则集 (NDIS) ](memory-usage-rule-set--ndis-.md) 
[其他规则集 (NDIS) ](miscellaneous-rule-set--ndis-.md) 
[OidProcessing 规则集 (NDIS) ](oidprocessing-rule-set--ndis-.md) 
**选择默认规则**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **默认**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

