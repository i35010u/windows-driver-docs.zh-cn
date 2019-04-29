---
title: 我的首选项选项卡
description: 本主题介绍 WDF 验证程序的我的首选项页。 在此页上，可以设置首选项对于某些控件面板的功能。
ms.assetid: 6f37fd6b-c60c-4d59-94fb-0dc7d3ff6f0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9245ab93209855704044f20a277a47ea3acb1fbe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363127"
---
# <a name="my-preferences-tab"></a>我的首选项选项卡


本主题介绍了 WDF Verifier**我的首选项**页。 在此页上，可以设置首选项对于某些控件面板的功能。

在顶部**我的首选项**选项卡上，您会发现**用户模式下调试程序首选项**框。

![我的首选项选项卡的屏幕抓图](images/wdfverifier-tab5.png)

调试程序在此页列出属于**有关 Windows 调试工具**。 若要下载此包，请选择**有关 Windows 调试工具**框在安装时[Windows 8.1 的 Windows SDK](https://go.microsoft.com/fwlink/p/?LinkId=733744)。 或者，选择通过选择自定义的 (非 Microsoft) 调试器**使用自定义**。

首先单击**选择特定的调试程序**按钮并浏览至用户模式下调试程序要使用。 **有关 Windows 调试工具**到 c： 默认情况下将安装\\Program Files (x86)\\Windows 工具包\\8.1\\调试器\\ *&lt;x86 |x64&gt;*。 调试器的列表显示为灰色 if**调试器路径**未指定有效路径。

调试器首选项可在两种情况下：

-   WDF 验证程序会自动尝试连接时如果选择了启动新的驱动程序主机进程用户模式调试器**自动启动请求时的用户模式下调试器**框[全局 WDF设置](global-wdf-settings-tab.md)页。
-   当您单击**用户模式调试器附加到此进程**按钮 (同样，在[全局 WDF 设置](global-wdf-settings-tab.md)选项卡)，WDF 验证程序尝试连接到指定的主机进程的用户模式下调试程序。

如果选择**自定义命令行**框中，将指定的字符串与任何调试器您已选择的 WDF 验证程序传递。

有关 Windows 调试工具调试程序默认命令行绕过初始中断、 将附加到特定的 PID，并指示调试器从进程中分离，并将它关闭调试器时运行。 用于为 Microsoft 提供的调试器命令行选项的完整列表，请参阅[命令行选项](https://msdn.microsoft.com/library/windows/hardware/ff539174)。

此外可以更改默认设置。 例如：

```
-g -pd -server npipe:pipe=wudf_%u -p %u
```

上面的命令行生成主机进程的 PID 上基于每个主机实例的唯一的服务器名称。 然后可以使用远程用户模式下调试的服务器名称。

如果指定自定义调试器 (一个不在为 Windows 调试工具包)，您必须为其提供自定义的命令行。

在此屏幕上，您还可以选择是否显示工具提示，如果是，多长时间。

最后，可以选择希望 WDF 验证程序时必须重新启动计算机、 UMDF 主机进程重新启动或设备重启的设置才能生效。

如果需要干预，并且您选择了**报告所需的操作和要求的权限**，会显示以下对话框：

![若要使更改生效所需的操作方的屏幕截图](images/wdfverifier-reboot-dialog.png)

所选的项是以使所有的更改生效所需的操作。 不能切换所选内容。

所选内容显示为一个指南，以防你想要单击**否**并手动执行的步骤。 操作的显示的顺序是应在其中执行它们的顺序。

如果您选择**不能要求提供同样的权限...** 框中，所选仍然存在除非更改我的首选项选项卡上的重新启动设置。

 

 





