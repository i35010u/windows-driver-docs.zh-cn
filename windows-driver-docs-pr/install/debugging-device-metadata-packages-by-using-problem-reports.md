---
title: 使用问题报告调试设备元数据包
description: 使用问题报告调试设备元数据包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b87f77bb1ef9d7cc6243db1370050a5047301611
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827767"
---
# <a name="debugging-device-metadata-packages-by-using-problem-reports"></a>使用问题报告调试设备元数据包


从 Windows 7 开始，操作系统会将有关设备元数据包错误的问题报告发送 (错误代码 0x50000xx) 到 Windows 错误报告 (WER) 服务器。 这些报告提供有用的调试信息，有助于诊断设备元数据包的问题。

有关设备元数据包错误的详细信息，请参阅 [设备元数据错误代码](device-metadata-error-codes.md)。

你可以使用 "操作中心" 或 "事件查看器" 查看操作系统已发送或即将发送到 Windows 错误报告服务器的问题报告。

### <a name="viewing-problem-reports-by-using-action-center"></a><a href="" id="viewing-error-reports-through-problem-reports-and-solution"></a>使用操作中心查看问题报告

按照以下步骤使用操作中心查看设备元数据包错误报告：

1.  在 " **开始** " 菜单上，键入 "查看所有问题报告"，然后按 enter。

2.  选择要查看的问题报告。

    报表包含错误的详细信息。

### <a name="viewing-error-reports-by-using-event-viewer"></a><a href="" id="viewing-error-reports-through-event-viewer"></a>使用事件查看器查看错误报告

可以在事件查看器中查看问题报告。 请按照以下步骤使用事件查看器查看设备元数据包问题报表：

1.  在 " **开始** " 菜单上，右键单击 " **计算机**"，然后单击 " **管理**"。

2.  展开 " **系统工具** " 节点。

3.  展开，然后单击 " **事件查看器** " 节点。

4.  展开 " **Windows 日志** " 节点。

5.  右键单击 " **应用程序**"，然后单击 " **筛选当前日志**"。

6.  在 " **事件 ID** " 文本框中键入 "1001"，然后单击 **"确定**"。

    " **事件 ID** " 文本框是对话框中间处于 " &lt; 所有事件 id" 的默认内容的未标记的文本框 &gt; 。

### <a name="interpreting-a-problem-report"></a><a href="" id="interpreting-the-problem-report"></a>解释问题报告

每个设备元数据检索客户端问题报告都包含以下信息：

-   应用程序特定的错误代码。 有关这些错误代码的详细信息，请参阅 [设备元数据错误代码](device-metadata-error-codes.md)。

-   Win32 错误代码。

-   设备元数据包的源，即 [设备元数据存储区](device-metadata-store.md) 或 [设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

 

 





