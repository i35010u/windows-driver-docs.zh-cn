---
title: Te.Service
description: 某些 TAEF 功能，例如跨计算机测试执行和运行方式，需要安装并启动 Te.Service。
ms.assetid: 2F137748-865C-45de-8F60-B607EEB791C0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a5b22621058cc0ed4132759ab12606a01fc11d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369794"
---
# <a name="teservice"></a>Te.Service


某些 TAEF 功能，如[跨机器测试执行](cross-machine-execution.md)并[RunAs](runas.md)，需要安装并启动 Te.Service。

## <a name="span-idinstallingandstartingteservicespanspan-idinstallingandstartingteservicespaninstalling-and-starting-teservice"></a><span id="installing_and_starting_te.service"></span><span id="INSTALLING_AND_STARTING_TE.SERVICE"></span>安装和启动 Te.Service


-   请确保 Wex.Services.exe、 Wex.Common.dll 和 Wex.Communication.dll 所有存在的相同目录中。 默认位置是\\测试\\运行时\\WDK 的 TAEF 子目录
-   从提升的命令提示符，键入以下命令：

    ``` syntax
    cd [your Wex.Services.exe directory]
    Wex.Services.exe /install:Te.Service
    sc start Te.Service
    ```

    **请注意**上 CoreSystem Te.Service 可作为控制台应用程序而不是一项服务运行。




``` syntax
cd [your Wex.Services.exe directory]
Wex.Services.exe /run:Te.Service
```


## <a name="span-idstoppingandremovingteservicespanspan-idstoppingandremovingteservicespanstopping-and-removing-teservice"></a><span id="stopping_and_removing_te.service"></span><span id="STOPPING_AND_REMOVING_TE.SERVICE"></span>停止和删除 Te.Service


-   从提升的命令提示符，键入以下命令：

    ``` syntax
    cd [your Wex.Services.exe directory]
    sc stop Te.Service
    Wex.Services.exe /remove:Te.Service
    ```

    在 CoreSystem，关闭运行 Te.Service 的控制台应用程序。

## <a name="span-idprocessorarchitecturessupportedspanspan-idprocessorarchitecturessupportedspanspan-idprocessorarchitecturessupportedspanprocessor-architectures-supported"></a><span id="Processor_Architectures_Supported"></span><span id="processor_architectures_supported"></span><span id="PROCESSOR_ARCHITECTURES_SUPPORTED"></span>支持的处理器体系结构


Te.Service 的 x86 和 x64 版本支持正在执行的 x86 和 x64 测试。

## <a name="span-idsafemodeinstallationinstructionsspanspan-idsafemodeinstallationinstructionsspanspan-idsafemodeinstallationinstructionsspansafe-mode-installation-instructions"></a><span id="Safe_Mode_Installation_Instructions"></span><span id="safe_mode_installation_instructions"></span><span id="SAFE_MODE_INSTALLATION_INSTRUCTIONS"></span>安全模式下安装说明


默认情况下，你将无法再在安全模式下启动服务。 当你尝试运行 sc start Te.Service 时，您将收到以下错误：错误 1084年:不能在安全模式下启动此服务和此错误是 (Windows) 设计使然。

若要启用 TAEF 服务安全模式功能，需要：

-   重新启动计算机，通过在 Windows 启动画面之前按 F8，在安全模式下。
-   单击“开始”，再单击“运行”，键入 regedit，然后单击“确定”。
-   找到并单击以下注册表子项：
    -   HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\安全引导\\最小 （适用于纯安全模式）
    -   HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\安全引导\\网络 （对于具有网络的安全模式）
-   在编辑菜单上指向新建，单击密钥，，然后键入 Te.Service。
-   双击默认在值的数据框中，键入服务，然后单击确定。
-   退出注册表编辑器，然后重新启动计算机。
-   使用提升权限打开命令窗口。
-   现在应已成功启动服务使用 sc 启动 Te.Service

## <a name="span-idsubscribingtonotificationsspanspan-idsubscribingtonotificationsspanspan-idsubscribingtonotificationsspansubscribing-to-notifications"></a><span id="Subscribing_to_Notifications"></span><span id="subscribing_to_notifications"></span><span id="SUBSCRIBING_TO_NOTIFICATIONS"></span>璹綷硄


在开发服务器运行测试时，您可以为一种类似于 HandlerEx 回调函数中的某些服务器通知订阅。 目前，只有服务\_控制\_支持 SESSIONCHANGE 控制代码。

订阅：

-   定义具有 HandlerEx 回调函数的签名的回调函数。
-   注册此函数使用 TAEF 通知 API
-   当你不再想要接收通知时，取消注册此函数。
-   将你的代码链接到 Te.Common.lib

例如：

```cpp
    // define a call back function
    DWORD WINAPI HandlerEx(DWORD dwControl, DWORD dwEventType, LPVOID, LPVOID)
    {
        // Do some work here
        return 0;
    }

    // register the callback function to receive notifications
    TestNotification::RegisterHandler(HandlerEx));
```









