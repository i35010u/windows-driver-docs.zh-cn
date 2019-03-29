---
title: WDF 验证
description: WDF 验证驱动程序验证程序。
ms.assetid: 9ee72369-878f-4710-a38b-1c93042178bd
keywords:
- WDF 验证驱动程序验证程序。
ms.date: 09/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50c300f799b477fc353b70c5ea693bfbeeeb549f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564309"
---
# <a name="wdf-verification"></a>WDF 验证

WDF 验证检查的内核模式驱动程序是否正在关注[内核模式驱动程序框架 (KMDF) 要求](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)正确。  

此验证失败将导致检查[bug 检查 0x10D:WDF_VIOLATION](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)。 


### <a name="activating-this-option"></a>激活此选项：

您可以激活端口/微型端口接口使用驱动程序验证程序管理器或 Verifier.exe 命令行检查一个或多个驱动程序。 有关详细信息，请参阅[选择 driver verifier 选项](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)。 必须重新启动计算机以激活或停用检查选项的微型端口端口/接口。

* **在命令行**

    在命令行中，在由表示端口微型端口接口检查**0x00100000**。 例如：
    
    `verifier /flags 0x00100000 /driver MyDriver.sys`

    在下一次启动后，该功能将处于活动状态。

* **使用驱动程序验证程序管理器**

1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入验证程序。
2. 选择创建自定义设置 （适用于代码开发人员），然后单击下一步。
3. Select(check) 端口微型端口接口检查。
4. 重新启动计算机。
