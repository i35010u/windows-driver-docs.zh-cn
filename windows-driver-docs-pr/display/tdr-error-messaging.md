---
title: TDR 错误消息传送
description: TDR 错误消息传送
ms.assetid: 0a29c701-2257-478d-bf2d-ca4a7edecfd0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01f3535a3ed9a6d35b63aea7eee7f95c1ab1e877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521016"
---
# <a name="tdr-error-messaging"></a>TDR 错误消息传送


在整个 TDR 过程 （即，检测和 GPU 停止操作的情况下从恢复的过程） 中，桌面是无响应，从而向最终用户不可用。 在恢复的最后一个阶段，简要屏幕闪烁可能类似于当最终用户更改屏幕分辨率时发生简要屏幕闪烁。 操作系统已成功恢复桌面后，向最终用户显示以下信息性消息。

![通知的屏幕截图的"显示驱动程序导致响应停止和已恢复"](images/tdr-error.png)

操作系统还前面的消息记录在事件查看器应用程序并收集诊断信息的调试报告形式。 如果最终用户在选择要提供反馈，操作系统会返回此调试报告给 Microsoft 通过在线崩溃分析 (OCA) 机制中。

 

 





