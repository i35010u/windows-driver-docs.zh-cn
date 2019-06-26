---
title: 开始使用 TAEF
description: 测试创作和执行框架 (TAEF) 入门
ms.assetid: 7F57C5EF-141A-4303-9B9F-2EC118324BF8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b5f505d2cfdf9786fb7acc19764a144e8df21b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373012"
---
# <a name="getting-started"></a>入门


## <a name="installation"></a>安装


当你安装[Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)，TAEF 文件放置在测试\\运行时\\TAEF WDK 的子目录。 当您设置测试计算机以进行部署，以下说明[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))，TAEF 文件安装在测试计算机上。

此外可以安装 TAEF 文件手动，请参阅[手动安装，并在测试计算机上卸载 TAEF](#manually-installing-and-uninstalling-taef-on-a-test-computer)。

## <a name="authoring-tests"></a>创作测试


TAEF 不限制通过本机或托管的关联用户。 用户可以创作测试时选择的最高效的语言。 TAEF 支持用 C 编写测试 /C++， C#，JScript 和 VBScript。

有关详细信息，请参阅[创作测试](authoring-tests.md)。

## <a name="executing-tests"></a>执行测试


执行测试是只需将测试文件在命令提示符下的传递给"TE.exe"工具的一种情况。 例如，运行以下命令：

``` syntax
TE.exe UnitTests\Wex.Common.Tests.dll
```

有关详细信息，请参阅[执行测试](executing-tests.md)。

## <a name="manually-installing-and-uninstalling-taef-on-a-test-computer"></a>手动安装和测试计算机上卸载 TAEF


如果你想要在计算机上运行测试，而无需使用 WDK 和 Visual Studio，请按照以下过程。

**若要手动安装 TAEF**

1.  在用于开发的计算机上安装 Visual Studio 和 WDK。
2.  TAEF 安装将所有文件都复制到测试计算机安装 WDK 其中的计算机。 TAEF 安装文件 (\*.msi 并\*.cab 文件) 位于 %programfiles%\\Windows 工具包\\8.0\\测试\\开发系统上的运行时目录。
3.  在测试计算机上，打开命令提示符窗口并导航到包含你刚才复制的 TAEF 安装文件的目录。 运行以下命令以安装 TAEF。 运行\*测试计算机的体系结构匹配的.msi 文件。

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi"
    ```

    -或者-

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x86-x86_en-us.msi"
    ```

    这将安装到 TAEF 文件\\Program Files\\Windows 工具包\\8.0\\测试\\运行时\\TAEF\\测试系统上。

**若要手动卸载 TAEF**

1.  停止 Te.Service。 打开 Microsoft 管理控制台 (compmgmt.msc)。 转到服务和应用程序\\服务，并找到 Te.Service。 右键单击 Te.Service，然后单击**停止**。
2.  转到控制面板\\程序\\程序和功能和卸载**测试创作和执行框架程序**。

 

 





