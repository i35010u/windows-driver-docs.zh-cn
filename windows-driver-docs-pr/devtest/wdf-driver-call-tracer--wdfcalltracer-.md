---
title: WDF 驱动程序调用跟踪程序 (WdfCallTracer)
description: WDF 驱动程序调用跟踪程序 (WdfCallTracer)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb9572475252e61015d2475f31e6e97b7a2ba81c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823347"
---
# <a name="wdf-driver-call-tracer-wdfcalltracer"></a>WDF 驱动程序调用跟踪程序 (WdfCallTracer)


你可以使用 WdfCallTracer 实时跟踪和查看与框架的驱动程序通信。 WdfCallTracer 是功能的名称，而不是单独的可执行文件， (此 ) 没有单独的二进制文件。

使用此功能，您可以实时查看 DDI 和事件调用。

以下过程说明了如何使用 KMDF 静态总线驱动程序示例的驱动程序通信来配置 WdfTester，该示例 ( 在 WDK) 中可用的 # A0。 目前只能查看 DDI 调用。

**设置 WDF 驱动程序调用跟踪器并生成示例驱动程序**

1.  安装 [WdfTester 安装](wdftester-installation.md)。

2.   ( # A0) 生成 KMDF 静态总线驱动程序示例。 KMDF 示例位于 *% WDKRoot%* \\ src \\ general \\ toaster \\ toastDrv \\ KMDF \\ bus \\ static directory 中。

3.  将总线驱动程序示例复制到包含已安装的 WdfTester 文件的目录。 按照 KMDF Toaster 示例的说明加载驱动程序。 使用 [DevCon](devcon.md) ( # A0) 或 " **添加新硬件" 向导**。

使用以下过程来配置 TraceView，以便可以实时查看 DDI 和事件调用

**在 TraceView 中创建新的日志会话**

1.  启动 TraceView.exe (*% WDKRoot%* \\ 工具 \\ *&lt; 平台 &gt;*) 。

2.  在 " **文件** " 菜单中，单击 " **创建新的日志会话**"。

3.  在 " **创建新的日志会话** " 对话框中，单击 " **添加提供程序**"。

4.  在 " **提供程序控制 Guid 设置** " 对话框中，单击 " **CTL (控件 GUID) 文件**"。

5.  单击 " **浏览** " 按钮，并从包含 Wdftester 文件和驱动程序的目录中选择 Wdftester 文件。

6.  单击 **“确定”** 。

7.  在 " **格式信息源" 选择** 对话框中，单击 " **选择 TMF 文件**"，然后单击 **"确定"**。

8.  在 " **跟踪格式信息设置** " 对话框中，单击 " **添加"，** 然后浏览到 WdfTester 文件所在的目录。

9.  单击 "Wdftester" tmf，单击 " **打开** " 以选择该文件，然后单击 " **完成**"。

10. 单击 "**创建新的日志会话**" 对话框中的 "**下一步**"，然后单击 "**完成**"。

现在，你已准备好注册驱动程序并启用跟踪功能，以便你可以查看驱动程序通信。

**注册 KMDF 驱动程序并启用跟踪**

1.  打开 "命令提示符" 窗口，并切换到安装 Wdftester 文件的目录。

2.  在此示例中注册 KMDF 驱动程序 (，Statbus.sys 使用 .wsf 脚本) 。
    ```
    cscript WdftesterScript.wsf register statbus.sys
    ```

3.  启用设备管理器的驱动程序，或插入硬件。 如果已启用了驱动程序，请使用设备管理器禁用该驱动程序，然后重新启用它。

你现在应在 TraceView 应用程序中看到驱动程序通信。

 

 





