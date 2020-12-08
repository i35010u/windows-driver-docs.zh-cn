---
title: Te.Service
description: 某些 TAEF 功能（如跨计算机测试执行和运行方式）需要安装和启动该服务。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6442f6b3251fc156d943b83538f04a5744712c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796385"
---
# <a name="teservice"></a>Te.Service


某些 TAEF 功能（如 [跨计算机测试执行](cross-machine-execution.md) 和 [运行](runas.md)方式）需要安装和启动该服务。

## <a name="span-idinstalling_and_starting_teservicespanspan-idinstalling_and_starting_teservicespaninstalling-and-starting-teservice"></a><span id="installing_and_starting_te.service"></span><span id="INSTALLING_AND_STARTING_TE.SERVICE"></span>正在安装和启动 Te 服务


-   确保 Wex.Services.exe、Wex.Common.dll 和 Wex.Communication.dll 都存在于同一目录中。 默认位置是 WDK 的 \\ 测试 \\ 运行时 \\ TAEF 子目录
-   在提升的命令提示符下键入以下命令：

    ``` syntax
    cd [your Wex.Services.exe directory]
    Wex.Services.exe /install:Te.Service
    sc start Te.Service
    ```

    **注意**  在 CoreSystem 上，Te 可作为控制台应用程序而不是服务运行。




``` syntax
cd [your Wex.Services.exe directory]
Wex.Services.exe /run:Te.Service
```


## <a name="span-idstopping_and_removing_teservicespanspan-idstopping_and_removing_teservicespanstopping-and-removing-teservice"></a><span id="stopping_and_removing_te.service"></span><span id="STOPPING_AND_REMOVING_TE.SERVICE"></span>停止并删除 Te 服务


-   在提升的命令提示符下键入以下命令：

    ``` syntax
    cd [your Wex.Services.exe directory]
    sc stop Te.Service
    Wex.Services.exe /remove:Te.Service
    ```

    在 CoreSystem 上，关闭运行 Te 的控制台应用程序。

## <a name="span-idprocessor_architectures_supportedspanspan-idprocessor_architectures_supportedspanspan-idprocessor_architectures_supportedspanprocessor-architectures-supported"></a><span id="Processor_Architectures_Supported"></span><span id="processor_architectures_supported"></span><span id="PROCESSOR_ARCHITECTURES_SUPPORTED"></span>支持的处理器体系结构


支持 x86 和 x64 版本的 Te 都支持 x86 和 x64 测试。

## <a name="span-idsafe_mode_installation_instructionsspanspan-idsafe_mode_installation_instructionsspanspan-idsafe_mode_installation_instructionsspansafe-mode-installation-instructions"></a><span id="Safe_Mode_Installation_Instructions"></span><span id="safe_mode_installation_instructions"></span><span id="SAFE_MODE_INSTALLATION_INSTRUCTIONS"></span>安全模式安装说明


默认情况下，你将不能在安全模式下启动该服务。 当你尝试运行 sc start Te 服务时，你将收到以下错误：错误1084：无法在安全模式下启动此服务，此错误是 (Windows) 设计的。

若要启用 TAEF service Safe 模式功能，你需要：

-   在 Windows 初始屏幕之前按 F8，在安全模式下重新启动计算机。
-   单击“开始”、“运行”，键入 regedit，然后单击“确定”。
-   找到并单击以下注册表子项：
    -   HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Control \\ SafeBoot \\ (纯安全模式) 
    -   HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Control \\ SafeBoot \\ Network (，适用于带网络) 的安全模式
-   在 "编辑" 菜单上，指向 "新建"，单击 "项"，然后键入 "Te. Service"。
-   双击 "默认值"，在 "值数据" 框中键入 "Service"，然后单击 "确定"。
-   退出注册表编辑器，然后重新启动计算机。
-   使用提升权限打开命令窗口。
-   现在应使用 sc start Te 成功启动服务

## <a name="span-idsubscribing_to_notificationsspanspan-idsubscribing_to_notificationsspanspan-idsubscribing_to_notificationsspansubscribing-to-notifications"></a><span id="Subscribing_to_Notifications"></span><span id="subscribing_to_notifications"></span><span id="SUBSCRIBING_TO_NOTIFICATIONS"></span>订阅通知


当开发服务器运行测试时，可以使用类似于 HandlerEx 回调函数的方式订阅某些服务器通知。 目前仅 \_ 支持服务控制 \_ SESSIONCHANGE 控制代码。

订阅：

-   使用 HandlerEx 回调函数的签名定义回调函数。
-   使用 TAEF 通知 API 注册此函数
-   如果不再希望收到通知，请注销此函数。
-   将代码链接到 Te Common .lib

示例：

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









