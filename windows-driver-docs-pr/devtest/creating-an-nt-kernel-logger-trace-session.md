---
title: 创建 NT 内核记录器跟踪会话
description: 创建 NT 内核记录器跟踪会话
ms.assetid: 606156b9-8ad9-4510-9929-4f0e3b7a3134
keywords:
- 跟踪会话 WDK，NT 内核记录器
- NT 内核记录器跟踪会话 WDK
- Windows 内核跟踪提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 977319c35e40e713e6cbe02cc4b569d1aeee0369
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380971"
---
# <a name="creating-an-nt-kernel-logger-trace-session"></a>创建 NT 内核记录器跟踪会话

## <span id="ddk_create_a_real_time_nt_kernel_logger_trace_session_tools"></span><span id="DDK_CREATE_A_REAL_TIME_NT_KERNEL_LOGGER_TRACE_SESSION_TOOLS"></span>

可以使用 TraceView 创建[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，记录生成的 Windows 内核的事件的 Windows 中内置的跟踪会话。

在创建 NT 内核记录器跟踪会话时，可以选择系统事件，例如"过程"的类别。 TraceView 配置跟踪会话，在该类别中记录所有系统事件。

### <a name="span-idtocreateanntkernelloggertracesessionspanspan-idtocreateanntkernelloggertracesessionspanto-create-an-nt-kernel-logger-trace-session"></a><span id="to_create_an_nt_kernel_logger_trace_session"></span><span id="TO_CREATE_AN_NT_KERNEL_LOGGER_TRACE_SESSION"></span>若要创建 NT 内核记录器跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**。

4.  单击**内核记录器**，选择一个或多个复选框，标识 NT 内核记录器会话事件类型，然后单击**确定**。

5.  在中**打开**对话框框中，找到 System.tmf，系统事件的跟踪消息格式 (TMF) 文件。 在工具 WDK 中包含 System.tmf\\跟踪子目录。

6.  若要添加的任何类型的其他提供程序，请单击**添加提供程序**。 此步骤可选。

7.  单击“下一步” 。

8.  [设置会话选项的基本跟踪](setting-basic-trace-session-options.md)，如果所需的。

9.  [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)，如果所需的。

10. 单击 **“完成”**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

NT 内核记录器跟踪会话的列表中将出现**名为提供程序选择**对话框与"Windows 内核跟踪。" 你可以使用**名为提供程序所选内容**对话框中或**内核记录器**选项**提供程序控件 GUID 安装程序**对话框来创建 NT 内核记录器跟踪会话。 但是，仅**提供程序控件 GUID 安装**对话框，可以选择要跟踪的内核组件。 有关使用详细信息**名为提供程序所选内容**对话框中，请参阅[为注册的提供程序创建跟踪会话](creating-a-trace-session-for-a-registered-provider.md)。
