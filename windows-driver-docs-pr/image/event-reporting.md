---
title: 事件报告
description: 事件报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06cbf1b6a3a47176b5b65eb2f16f6e7d09477ef6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816727"
---
# <a name="event-reporting"></a>事件报告





当设备上的某些操作发生时，WIA 体系结构使静止图像设备通知 WIA 微型驱动程序。 例如，扫描仪的前面板上可能会有一个按钮，使用户能够直接从设备启动扫描。 WIA 微型驱动程序必须收到此事件的通知，以便它可以通知 WIA 服务。 已注册接收此事件的所有正在运行的应用程序都将收到通知。 此外，如果应用程序已注册为在事件发生之前作为此事件启动，WIA 服务将启动该应用程序。

WIA 体系结构支持中断事件和轮询事件。 有关这些事件的详细信息，请参阅 [WIA 驱动程序事件支持](wia-driver-event-support.md)。

 

 




