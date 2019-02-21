---
title: 检查端口/微型端口接口
description: 检查端口/微型端口接口
ms.assetid: ad6c4762-354d-446d-bcda-a2e99c37c589
keywords:
- 检查端口/微型端口接口
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f71ea841e0304bb0c9924b99098a4307b789f61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543224"
---
# <a name="portminiport-interface-checking"></a>检查端口/微型端口接口

检查端口/微型端口接口使驱动程序验证程序检查 PortCls.sys 和其音频微型端口驱动程序，以及 ks.sys 和其 AVStream 微型端口驱动程序之间的 DDI 接口。 请参阅[AVStream 驱动程序的规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-avstream-drivers)和[音频驱动程序的规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-audio-drivers)

### <a name="activating-this-option"></a>激活此选项：

您可以激活端口/微型端口接口使用驱动程序验证程序管理器或 Verifier.exe 命令行检查一个或多个驱动程序。 有关详细信息，请参阅[选择 driver verifier 选项](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)。 必须重新启动计算机以激活或停用检查选项的微型端口端口/接口。

* **在命令行**

    在命令行中，在由表示端口微型端口接口检查**0x0 x 00010000 (16 位)**。 例如：
    
    `verifier /flags 0x00010000 /driver MyDriver.sys`

    在下一次启动后，该功能将处于活动状态。

* **使用驱动程序验证程序管理器**

1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入验证程序。
2. 选择创建自定义设置 （适用于代码开发人员），然后单击下一步。
3. Select(check) 端口微型端口接口检查。
4. 重新启动计算机。
