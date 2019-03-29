---
title: WDF 驱动程序调用跟踪程序 (WdfCallTracer)
description: WDF 驱动程序调用跟踪程序 (WdfCallTracer)
ms.assetid: 67ad4b5e-9117-435e-bd81-90069a806d3c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 379c8665120c5b94e0935a7ff6ab35cf7c2e2cfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569077"
---
# <a name="wdf-driver-call-tracer-wdfcalltracer"></a>WDF 驱动程序调用跟踪程序 (WdfCallTracer)


您可以使用 WdfCallTracer 与在真实时间框架的跟踪和查看驱动程序通信。 WdfCallTracer 是一项功能和不 （没有对此没有单独的二进制文件。） 的独立可执行文件的名称。

使用此功能，可以查看 DDI 并在真实时间中调用的事件。

以下过程演示如何可以通过用于 KMDF 静态总线驱动程序示例 (Statbus.sys WDK 中提供) 的驱动程序通信配置 WdfTester。 当前仅 DDI 调用可以进行查看。

**若要设置 WDF 驱动程序调用跟踪和生成的示例驱动程序**

1.  安装[WdfTester 安装](wdftester-installation.md)。

2.  构建 KMDF 静态总线驱动程序示例 (Statbus.sys)。 KMDF 示例位于 *%wdkroot%*\\src\\常规\\toaster\\toastDrv\\kmdf\\总线\\静态目录。

3.  将总线驱动程序示例复制到包含您安装的 WdfTester 文件的目录。 加载驱动程序按照 KMDF Toaster 示例的说明。 使用[DevCon](devcon.md) (Devcon.exe) 或**添加新硬件向导**。

使用以下过程来配置 TraceView，以便你可以查看 DDI 并在真实时间中调用事件

**若要在 TraceView 中创建一个新的日志会话**

1.  启动 TraceView.exe (*%wdkroot%*\\工具\\*&lt;平台&gt;*)。

2.  从**文件**菜单上，单击**新建日志会话**。

3.  在中**新建日志会话**对话框中，单击**添加提供程序**。

4.  在中**提供程序控件 GUID 安装程序**对话框中，单击**CTL (控制 GUID) 文件**。

5.  单击**浏览**按钮，然后选择 Wdftester.ctl 文件包含 WdfTester 文件和您的驱动程序的目录中。

6.  单击 **“确定”**。

7.  在中**格式的信息源选择**对话框中，单击**选择 TMF 文件**，然后单击**确定**。

8.  在中**跟踪格式的信息安装程序**对话框中，单击**外，** ，然后浏览到 WdfTester 文件所在的目录。

9.  单击 Wdftester.tmf，再单击**开放**以选择该文件，然后单击**完成**。

10. 单击**下一步**中**新建日志会话**对话框中，然后单击**完成**。

现在已准备好注册驱动程序，并启用跟踪，以便可以查看驱动程序通信。

**若要注册 KMDF 驱动程序，并启用跟踪**

1.  打开命令提示符窗口，并将更改为安装 Wdftester 文件的目录。

2.  使用 WdftesterScript.wsf 脚本注册 KMDF 驱动程序 （在此示例中，Statbus.sys）。
    ```
    cscript WdftesterScript.wsf register statbus.sys
    ```

3.  启用驱动程序从设备管理器中，或插入您的硬件。 如果已启用您的驱动程序，使用设备管理器禁用它，，然后再次启用它。

现在应看到 TraceView 应用程序中的驱动程序通信。

 

 





