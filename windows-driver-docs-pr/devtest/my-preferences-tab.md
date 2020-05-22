---
title: 我的首选项选项卡
description: 本主题介绍 WDF 验证器的 "我的首选项" 页。 在此页上，您可以为某些 "控制面板" 功能设置首选项。
ms.assetid: 6f37fd6b-c60c-4d59-94fb-0dc7d3ff6f0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2b12a17d7d1376402a62bc154db0528bf1c8d07
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769659"
---
# <a name="my-preferences-tab"></a>我的首选项选项卡


本主题介绍 WDF 验证器的 **"我的首选项"** 页。 在此页上，您可以为某些 "控制面板" 功能设置首选项。

在 "**我的首选项**" 选项卡的顶部，可以找到 "**用户模式调试器首选项**" 框。

!["我的首选项" 选项卡的屏幕截图](images/wdfverifier-tab5.png)

此页上列出的调试器是**适用于 Windows 的调试工具**的一部分。 若要下载此包，请在安装[Windows 8.1 的 Windows SDK](https://developer.microsoft.com/windows/downloads/sdk-archive/)时选择 "适用于**Windows 的调试工具**" 框。 或者，通过选择 "**使用自定义**" 来选择自定义（非 Microsoft）调试器。

首先，单击 "**选择特定的调试器**" 按钮，然后浏览到要使用的用户模式调试器。 **Windows 的调试工具**默认安装到 C： \\ Program Files （x86） \\ Windows 工具包 \\ 8.1 \\ 调试器 \\ * &lt; x86 | x64 &gt; *。 如果**调试器的路径**未指定有效路径，则调试器列表将灰显。

调试器首选项在两种情况下使用：

-   如果已在 "[全局 WDF 设置](global-wdf-settings-tab.md)" 页上选择 "**请求时自动启动用户模式调试器**" 框，则当新的驱动程序主机进程启动时，WDF 验证程序会自动尝试连接用户模式调试器。
-   当你单击 "**将用户模式调试器附加到此进程**" 按钮（也在 "[全局 WDF 设置](global-wdf-settings-tab.md)" 选项卡上）时，WDF 验证程序会尝试将用户模式调试器连接到指定的主机进程。

如果选择 "**自定义命令行**" 框，WDF 验证程序会将指定的字符串传递给所选的任何调试器。

用于 Windows 调试器的调试工具的默认命令行会绕过初始中断，附加到特定 PID，并指示调试器与进程分离，并在关闭调试器时使其保持运行。 有关 Microsoft 提供的调试程序的命令行选项的完整列表，请参阅[命令行选项](https://docs.microsoft.com/windows-hardware/drivers/debugger/command-line-options)。

你还可以更改默认设置。 例如：

```
-g -pd -server npipe:pipe=wudf_%u -p %u
```

上述命令行将基于主机进程的 PID 为每个主机实例生成唯一的服务器名称。 然后，你可以将服务器名称用于远程用户模式调试。

如果指定自定义调试器（不在 Windows 包的调试工具中），则必须为其提供自定义命令行。

在此屏幕上，还可以选择是否显示工具提示，如果需要，还可以选择是否显示时间长度。

最后，可以选择在必须重新启动计算机、启动 UMDF 主机进程或设备循环以使设置生效时要执行的 WDF 验证程序。

如果需要干预，并且您已选择了所**需的报表操作并要求您提供权限**，则会显示以下对话框：

![屏幕截图，使更改生效所需的操作](images/wdfverifier-reboot-dialog.png)

选定的项是使所有更改生效所需的操作。 您无法切换所选内容。

选择内容将显示为指导，以防您单击 "**否**" 并手动执行这些步骤。 操作的显示顺序是执行这些操作的顺序。

如果选中 "不再**询问权限 ...** " 框，则你的选择将一直存在，除非你更改 "我的首选项" 选项卡上的 "重新启动" 设置。

 

 





