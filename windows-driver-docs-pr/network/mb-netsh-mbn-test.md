---
title: netsh mbn 测试安装
description: Netsh mbn 测试安装
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 977b4b183d225b6b411cef8051baa6ec1a7954b1
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719464"
---
# <a name="netsh-mbn-test"></a>netsh mbn 测试
**netsh mbn test** 是一种独立于正常发布版本的测试工具包。
若要启用此功能，需要先将硬件实验室包安装 (HLK) 客户端。

## <a name="hlk"></a>HLK
安装在 DUT 中启用 **netsh mbn test** 函数的 [HLK 客户端](/windows-hardware/test/hlk/getstarted/step-2--install-client-on-the-test-system-s-)。

或者，你可以在 HLK 包 (path： installer\HLK-TAEF-TOOL-[] ) 中安装 [**Hlk Taef 工具**](../taef/index.md) ，以启用 **netsh mbn 测试**。

在所测试的设备上运行测试命令 (安装了 HLK 客户端的 DUT) 。

示例：
```
netsh mbn test feature=connectivity param="AccessString=internet"
```

## <a name="vhlk"></a>VHLK

还可以使用 [VHLK](/windows-hardware/test/hlk/getstarted/getstarted-vhlk) 客户端启用 DUT 中的 **netsh mbn test** 函数。

安装程序：在主机计算机上安装 VHLK，并从位置： C:\Program 个文件 (x86) \Windows Kits\10\Hardware Lab Kit\Tests\amd64\Net\logo\Wwan 运行脚本 ConfigureTestSetup.ps1 <DUT 的 IP>

然后，可以对 DUT 运行测试命令。 

示例：

```
netsh mbn test feature=connectivity param="AccessString=internet"
```