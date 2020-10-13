---
title: SIM 工具包概述
description: SIM 工具包概述
ms.assetid: 39869948-d61c-438c-a90c-05dcb099acad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a5ea9142aaea1a40a67cb4ef06b6533c15f0c50
ms.sourcegitcommit: db9d058a9e592d4c47c67fc14f04f0ddc3aa92af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91989857"
---
# <a name="sim-toolkit-overview"></a>SIM 工具包概述


SIM 工具包是 SIM 中的一组应用程序，可以通过网络事件或用户操作来激活。 SIM 工具包应用程序由3GPP 和 ETSI 规范定义的主动命令表示。 Windows 10 移动版支持 SIM 工具包的一个子集。 有关支持的命令的列表，请参阅 [SIM 工具包命令](sim-toolkit-commands.md)。

## <a name="sim-toolkit-components"></a>SIM 工具包组件


SIM 工具包的三个主要组件是：

-   调制解调器和无线电接口层 (芯片供应商提供的 RIL) 软件。

-   服务，它是本机代码的 DLL。

-   用户界面)  (UI。

SIM 套件服务和用户界面都由 Microsoft 提供。

下图说明了 SIM 工具包的主要组件。

![sim 工具包组件](images/sim-toolkit-components.png)

### <a name="sim-toolkit-service"></a>SIM 工具包服务

SIM 工具包服务是 Windows 10 移动版操作系统的一部分。 它作为后台任务运行，并充当 SIM 和 SIM 工具包 UI 应用程序之间的命令解释器。

### <a name="sim-toolkit-ui-application"></a>SIM 工具包 UI 应用程序

SIM 工具包 UI 按 SIM 工具包服务的指示显示文本。

SIM 工具包 UI 应用程序显示两种类型的文本字符串：

-   应用程序管理字符串是 SIM 工具包 UI 的一部分。 Microsoft 将这些字符串本地化为 Windows 支持的语言。

-   移动运营商提供作为与 SIM 交互的消息一部分显示的文本字符串。 Microsoft 不对这些文本字符串进行本地化。

SIM 工具包 UI 应用程序还可以播放声音并启动浏览器。

### <a name="sim-toolkit-customizations"></a>SIM 工具包自定义

如果默认值不满足移动运营商的要求，Oem 可以修改某些对话框或消息的显示时间。 MCSF 和 Windows 预配中提供了这些自定义设置，因此你可以选择要使用的方法。 默认显示时间如下所示：

-   GETINPUT T>：120秒

-   文字内容：60秒

-   SELECTITEM：60秒

-   GETINKEY：60秒

### <a name="example-of-processing-a-sim-toolkit-command"></a>处理 SIM 工具包命令的示例

下面是一个处理 SIM 工具包显示文本命令的示例：

-   SIM 发送显示文本命令。

-   SIM 工具包服务接收显示文本，并将该命令传递给 SIM 工具包 UI。

-   SIM 工具包 UI 显示文本字符串。

## <a name="starting-the-sim-toolkit-ui-application"></a>启动 SIM 工具包 UI 应用程序


安装 sim 工具箱 UI 应用程序时，"**设置**" 网络上将显示 " **sim 应用程序**" 按钮 &gt; **& 无线** &gt; **手机网络 & "sim** &gt; **高级选项**" 屏幕上。 若要启动应用程序，请点击 "" 按钮。

如果满足以下任一条件，则将隐藏 " **SIM 应用程序** " 按钮：

-   用于 2G SIM) 的 SIM 固定锁定 (

-   PUK (个人解锁密钥) 用于 2G SIM 的锁定 () 

-   SIM 中无 SIM 应用程序

-   无 SIM

当 SIM 工具包 UI 应用程序成功启动时，SIM 工具箱 UI 会显示用户要选择的选项。 这些选项由 SIM 上的应用程序确定。

## <a name="launching-the-sim-toolkit-using-another-app"></a>使用其他应用启动 SIM 工具包


为了更容易地发现 SIM 工具包，合作伙伴可以使用保留 URI 方案来启用 UWP 应用程序以启动 SIM 应用程序 CPL。 有关如何执行此操作的详细信息，请参阅 [用于启动 SIM 工具包的保留 URI](reserved-uri-to-launch-sim-toolkit.md)。

## <a name="sim-toolkit-ui-notifications"></a>SIM 工具包 UI 通知


如果在电话拨号器屏幕中收到 SIM 命令，则不会显示 SIM 应用程序 UI。 在这种情况下，屏幕顶部将显示一个通知 toast。 点击 toast 即可启动 SIM 应用程序 UI。 在所有其他情况下，将启动 SIM 工具包 UI 应用程序并将其显示在整个屏幕上。

## <a name="additional-reference"></a>其他参考


建议使用以下设置：

-   在运行测试时将锁定屏幕超时设置为 "从不"，以使锁定屏幕不会干扰测试。 默认情况下，它设置为1分钟。

-   对于 CDMA 设备，请确保设备上已设置了 APN。

-   某些测试套件的默认计时器值为90秒。 如果适用，请确保相应地设置超时自定义注册表值。

## <a name="related-topics"></a>相关主题


[SIM 工具包命令](sim-toolkit-commands.md)

 

