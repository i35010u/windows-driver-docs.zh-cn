---
title: 端口/微型端口接口检查
description: 端口/微型端口接口检查
keywords:
- 端口/微型端口接口检查
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b75e8bf17dce64a300d2e589f612bd712eef921
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832805"
---
# <a name="portminiport-interface-checking"></a>端口/微型端口接口检查

端口/微型端口接口检查使驱动程序验证程序能够检查 PortCls.sys 及其音频微型端口驱动程序之间的 DDI 接口，以及 ks.sys 及其 AVStream 微型端口驱动程序。 请参阅 [AVStream 驱动程序规则](./rules-for-avstream-drivers.md) 和 [音频驱动程序规则](./rules-for-audio-drivers.md)

### <a name="activating-this-option"></a>激活此选项：

可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行来为一个或多个驱动程序激活端口/微型端口接口检查。 有关详细信息，请参阅 [选择驱动程序验证程序选项](./selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用端口/微型端口接口检查选项。

* **在命令行中**

    在命令行中，端口微型端口接口检查由 **0x0x00010000 (位 16)** 表示。 例如：
    
    `verifier /flags 0x00010000 /driver MyDriver.sys`

    此功能将在下一次启动后处于活动状态。

* **使用驱动程序验证器管理器**

1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入 Verifier。
2. 选择 "为代码开发人员 (创建自定义设置") ，然后单击 "下一步"。
3. 选择 (检查) 端口微型端口接口检查。
4. 重新启动计算机。
