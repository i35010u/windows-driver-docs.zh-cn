---
title: 使用问题报告调试设备元数据包
description: 使用问题报告调试设备元数据包
ms.assetid: 303d1b08-1f1c-48ca-89a9-9087516fcd48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 756ee7eb302e6cde389d51141b469ceabd710e0e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545035"
---
# <a name="debugging-device-metadata-packages-by-using-problem-reports"></a>使用问题报告调试设备元数据包


操作系统从 Windows 7 开始，向 Windows 错误报告 (WER) 服务器发送设备元数据包错误 (错误代码 0x50000xx) 有关的问题报告。 这些报告提供有用的调试信息来帮助诊断你的设备元数据包的问题。

有关设备元数据包错误的详细信息，请参阅[设备元数据错误代码](device-metadata-error-codes.md)。

可以使用操作中心或事件查看器查看问题报告的操作系统已发送或将很快发送到 Windows 错误报告服务器。

### <a href="" id="viewing-error-reports-through-problem-reports-and-solution"></a>通过使用操作中心查看问题报告

请按照这些步骤通过使用操作中心查看设备元数据的包错误报告：

1.  上**启动**菜单中，键入"查看所有问题报告"，然后按 ENTER。

2.  选择您想要查看问题报告。

    报表包含错误的详细的信息。

### <a href="" id="viewing-error-reports-through-event-viewer"></a>使用事件查看器中查看错误报表

您可以在事件查看器中查看问题报告。 请按照下列步骤以使用事件查看器查看设备元数据包问题报告：

1.  上**启动**菜单中，右键单击**计算机**，然后单击**管理**。

2.  展开**系统工具**节点。

3.  展开，然后单击**事件查看器**节点。

4.  展开**Windows 日志**节点。

5.  右键单击**应用程序**，然后单击**筛选当前日志**。

6.  类型"1001"中的**事件 ID**文本框中，，然后单击**确定**。

    **事件 ID**文本框中是中间具有的默认内容对话框中的未标记的文本框"&lt;所有事件 Id&gt;"。

### <a href="" id="interpreting-the-problem-report"></a>解释问题报告

每个设备元数据检索客户端问题报告中包含以下信息：

-   特定于应用程序的错误代码。 有关这些错误代码的详细信息，请参阅[设备元数据错误代码](device-metadata-error-codes.md)。

-   Win32 错误代码。

-   设备元数据包，为源[设备元数据存储区](device-metadata-store.md)或[设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

 

 





