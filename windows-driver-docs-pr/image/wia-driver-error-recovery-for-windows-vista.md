---
title: WIA 驱动程序错误恢复
description: WIA 驱动程序错误恢复
ms.assetid: 7347cc02-e00e-418e-9ac4-8bfda7d02857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94479e94f3d91dac6983c5d627bc0eb1b826995
ms.sourcegitcommit: 67aadd2adef4c338b703464c377ae8c910f1f5f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67622671"
---
# <a name="wia-driver-error-recovery"></a>WIA 驱动程序错误恢复

在其中软件、 硬件或配置错误可能导致意外的延迟、 失败的消息或难以辨识挂起 WIA 映像采购流程中有多个点。 大多数错误出现在其中应用程序请求图像数据，预览或完整的映像的点。 

本部分介绍了一种机制，允许应用程序和用户正常地处理这些错误和延迟的影响，也可能从其恢复。 它不能解决时尝试设置或获取设备属性，或当插入驱动程序的回调例程永远不会返回，或在其他非传输相关的情况下提高错误恢复的方法。

本部分包括：

[WIA 错误处理体系结构](wia-error-handling-architecture.md)

[WIA 错误处理程序取消的无模式对话框](wia-error-handler-cancellation-of-modeless-dialogs.md)

[WIA 错误处理程序返回值](wia-error-handler-return-values.md)

[WIA 设备的消息](wia-device-messages.md)

[安装 WIA 的错误处理驱动程序扩展](installing-a-wia-error-handling-driver-extension.md)

[WIA 错误处理示例](wia-error-handling-example.md)

有关 WIA 错误宏的信息，请参阅[WIA 诊断日志宏](wia-diagnostic-log-macros.md)。
