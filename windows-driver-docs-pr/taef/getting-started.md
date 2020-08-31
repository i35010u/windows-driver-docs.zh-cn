---
title: 入门与 TAEF
description: '入门测试创作和执行框架 (TAEF) '
ms.assetid: 7F57C5EF-141A-4303-9B9F-2EC118324BF8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93a436ff4bd06351e56fbebd42a398aa2af2e035
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056963"
---
# <a name="getting-started"></a>入门


## <a name="installation"></a>安装


安装 [Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)后，TAEF 文件将放在 WDK 的测试 \\ 运行时 \\ TAEF 子目录中。 设置测试计算机以进行部署时，按照说明为 [驱动程序部署设置计算机并测试 (wdk 8.1) ](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 或 [预配用于驱动程序部署和测试的计算机 (wdk 8) ](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))，在测试计算机上安装 TAEF 文件。

你还可以手动安装 TAEF 文件，请参阅 [在测试计算机上手动安装和卸载 TAEF](#manually-installing-and-uninstalling-taef-on-a-test-computer)。

## <a name="authoring-tests"></a>创作测试


TAEF 不会限制具有本机或托管相关性的用户。 创作测试时，用户可以选择最有效的语言。 TAEF 支持在 C/c + +、c #、JScript 和 VBScript 中编写测试。

有关详细信息，请参阅 [创作测试](authoring-tests.md)。

## <a name="executing-tests"></a>执行测试


执行测试只是在命令提示符下将测试文件传递到 "TE.exe" 工具的一种情况。 例如，运行以下内容：

``` syntax
TE.exe UnitTests\Wex.Common.Tests.dll
```

有关详细信息，请参阅 [执行测试](executing-tests.md)。

## <a name="manually-installing-and-uninstalling-taef-on-a-test-computer"></a>在测试计算机上手动安装和卸载 TAEF


如果要在不使用 WDK 和 Visual Studio 的计算机上运行测试，请执行此过程。

**手动安装 TAEF**

1.  在用于开发的计算机上安装 Visual Studio 和 WDK。
2.  将所有 TAEF 安装文件从安装了 WDK 的计算机复制到测试计算机。 TAEF 安装文件 (\* .msi 和 \* .cab 文件) 位于开发系统上的% programfiles% \\ Windows 工具包 \\ 8.0 \\ 测试 \\ 运行时目录中。
3.  在测试计算机上，打开命令提示符窗口并导航到包含刚才复制的 TAEF 安装文件的目录。 运行以下命令以安装 TAEF。 运行 \* 与测试计算机的体系结构匹配的 .msi。

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi"
    ```

    -或-

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x86-x86_en-us.msi"
    ```

    这将在测试系统上安装 TAEF 文件到 \\ Program files \\ Windows 工具包 \\ 8.0 \\ 测试 \\ 运行时 \\ TAEF \\ 。

**手动卸载 TAEF**

1.  停止 Te 服务。 打开 Microsoft 管理控制台 ("compmgmt.msc") 。 请参阅 "服务和应用程序 \\ 服务"，并找到 "Te" 服务。 选择并按住 (或右键单击 Te) ，然后选择 " **停止**"。
2.  中转到 "控制面板" "程序" "程序 \\ \\ 和功能"，然后卸载 **测试创作和执行框架程序**。

 

 





