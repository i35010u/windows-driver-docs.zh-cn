---
title: WIA 驱动程序错误恢复
description: WIA 驱动程序错误恢复
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 929c8c0a654d7bae8d67512ad0f44d8f4c8fc167
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818927"
---
# <a name="wia-driver-error-recovery"></a>WIA 驱动程序错误恢复

WIA 图像获取过程中有多个点，其中，软件、硬件或配置错误可能导致意外的延迟、失败消息或无法解读的挂起。 其中的大多数错误发生在应用程序请求图像数据的点（对于预览版）或用于完整映像。 

本部分介绍了一种机制，该机制使应用程序和用户能够正常处理这些错误和延迟，并可能会从中恢复它们。 它不会解决在尝试设置或获取设备属性时，或者在不返回回驱动程序的情况下或在其他非传输相关情况下的情况下，用于改进错误恢复的方法。

本节包括：

[WIA 错误处理体系结构](wia-error-handling-architecture.md)

[WIA 错误处理程序取消无模式对话框](wia-error-handler-cancellation-of-modeless-dialogs.md)

[WIA 错误处理程序返回值](wia-error-handler-return-values.md)

[WIA 设备消息](wia-device-messages.md)

[安装 WIA 错误处理驱动程序扩展](installing-a-wia-error-handling-driver-extension.md)

[WIA 错误处理示例](wia-error-handling-example.md)

有关 WIA 错误宏的信息，请参阅 [Wia 诊断日志宏](wia-diagnostic-log-macros.md)。
