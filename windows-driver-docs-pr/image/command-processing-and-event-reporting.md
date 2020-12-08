---
title: 命令处理和事件报告
description: 命令处理和事件报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8c48dde3b817176ea442e3b20cb75f1a73ad7c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790639"
---
# <a name="command-processing-and-event-reporting"></a>命令处理和事件报告





WIA 微型驱动程序可以支持源自 WIA 应用程序的命令请求，也可直接从 WIA 服务支持。 此外，某些静止图像设备可以通过用户操作将通知发送给驱动程序。 例如，当用户按下一个按钮时，具有一个或多个前面板按钮的扫描程序可以通知驱动程序。 此功能使驱动程序可以采取某种措施。 当驱动程序通知 WIA 服务已经按下某个特定按钮时，WIA 服务可以启动以前注册的应用程序来处理事件。

本节包含下列主题：

[命令处理](command-handling.md)

[事件报告](event-reporting.md)

 

 




