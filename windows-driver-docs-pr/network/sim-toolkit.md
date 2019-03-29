---
title: SIM 工具包
description: SIM 工具包
ms.assetid: 39869948-d61c-438c-a90c-05dcb099acad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 351dbe512f2009553db5ba0127db56d367b5fb10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568523"
---
# <a name="sim-toolkit"></a>SIM 工具包


SIM 工具包是一组可由用户操作或网络事件激活 SIM 上的应用程序。 SIM 工具包应用程序都是主动通过 3GPP 和 ETSI 规范所定义的命令。 Windows 10 移动版支持一小部分 SIM 工具包命令。 有关受支持的命令的列表，请参阅[SIM 工具包命令](sim-toolkit-commands.md)。

## <a name="sim-toolkit-components"></a>SIM 工具包组件


SIM 工具包的三个主要组件包括：

-   调制解调器和单选接口层 (RIL) 软件硅供应商提供的。

-   服务，它是本机代码的 DLL。

-   用户界面 (UI) 中。

这两种 SIM 工具包服务和用户界面是由 Microsoft 提供的。

下图说明了 SIM 工具包的主要组件。

![sim 工具包组件](images/sim-toolkit-components.png)

### <a name="sim-toolkit-service"></a>SIM 工具包服务

SIM 工具包服务是 Windows 10 移动操作系统的一部分。 它在运行作为后台任务，并充当 SIM 和 SIM 工具包 UI 应用程序之间的命令解释器。

### <a name="sim-toolkit-ui-application"></a>SIM 工具包 UI 应用程序

SIM 工具包 UI 显示文本的 SIM 工具包服务的指导。

SIM 工具包 UI 应用程序将显示两种类型的文本字符串：

-   应用程序管理字符串是 UI 的 SIM 工具包的一部分。 Microsoft 为 Windows 所支持的语言本地化这些字符串。

-   移动运营商提供与 SIM 的消息交互的一部分显示的文本字符串。 Microsoft 不会本地化这些文本字符串。

SIM 工具包 UI 应用程序还可以播放声音，并启动浏览器。

### <a name="sim-toolkit-customizations"></a>SIM 工具包自定义项

如果默认值不符合移动运营商的要求，Oem 可以修改某些对话框或消息的显示时间。 这些自定义设置是在 MCSF 和预配，因此您可以选择要使用的方法的 Windows 中可用。 默认显示时间如下所示：

-   GETINPUT:120 秒

-   显示文本：60 秒

-   SELECTITEM:60 秒

-   GETINKEY:60 秒

有关这些自定义的信息，请参阅[自定义 SIM 工具包](https://msdn.microsoft.com/library/windows/hardware/mt629102)。

### <a name="example-of-processing-a-sim-toolkit-command"></a>正在处理 SIM 工具包命令的示例

以下是处理 SIM 工具包的显示文本命令的示例：

-   Sim 卡发送的显示文本命令。

-   SIM 工具包服务接收的显示文本，并将该命令传递给 SIM 工具包 UI。

-   SIM 工具包 UI 显示的文本字符串。

## <a name="starting-the-sim-toolkit-ui-application"></a>启动 SIM 工具包 UI 应用程序


安装 SIM 工具包 UI 应用程序时， **SIM 应用程序**按钮将出现在**设置** &gt; **网络和无线** &gt;**移动电话和 SIM** &gt; **高级选项**屏幕。 若要启动该应用程序，请点击的按钮。

**SIM 应用程序**按钮处于隐藏状态，如果任何满足以下条件：

-   Sim 卡 PIN 锁定 （用于 2 G SIM)

-   PUK （个人解锁密钥） （适用于 2 G SIM) 锁定

-   Sim 卡上没有 sim 卡的应用程序

-   存在没有 SIM

已成功启动 SIM 工具包 UI 应用程序时，SIM 工具包用户界面显示供用户选择的选项。 Sim 卡上的应用程序由确定选项。

## <a name="launching-the-sim-toolkit-using-another-app"></a>启动使用另一个应用程序的 SIM 工具包


若要使 SIM 工具包更容易地发现，合作伙伴可以使用保留的 URI 方案启用 UWP 应用以启动 SIM 应用程序 CPL。 有关如何执行此操作的详细信息，请参阅[保留的 URI，以启动 SIM 工具包](reserved-uri-to-launch-sim-toolkit.md)。

## <a name="sim-toolkit-ui-notifications"></a>SIM 工具包 UI 通知


如果 SIM 命令收到电话拨号程序屏幕中，不会显示 SIM 应用程序 UI。 在这种情况下，通知 toast 通知显示在屏幕的顶部。 点击 toast 启动 SIM 应用程序 UI。 在所有其他情况下，SIM 工具包 UI 应用程序启动，并且整个屏幕上显示。

## <a name="additional-reference"></a>其他参考


建议使用以下设置：

-   运行测试，以便在锁定屏幕不会干扰测试时，锁定屏幕超时设置为从不。 默认情况下，它是设置为 1 分钟。

-   对于 CDMA 的设备，请确保在设备上设置此 APN。

-   某些测试套件有默认计时器值为 90 秒。 如果适用，请确保相应地设置超时自定义注册表值。

## <a name="related-topics"></a>相关主题


[SIM 工具包命令](sim-toolkit-commands.md)

 

 






