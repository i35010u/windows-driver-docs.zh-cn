---
title: 视频调试 KMDF 驱动程序
description: 本主题包含 Kumar Rajeev 的三部分视频系列的链接，演示如何调试内核模式驱动程序框架（KMDF）驱动程序。
ms.assetid: 62D0F1DA-318F-4989-94C5-968C67F420C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b76d614462b0105619dcdd2f5e6ec4bd182915
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210499"
---
# <a name="videos-debugging-kmdf-drivers"></a>视频：调试 KMDF 驱动程序


本主题包含 Kumar Rajeev 的三部分视频系列的链接，演示如何调试内核模式驱动程序框架（KMDF）驱动程序。

观看视频后，您将熟悉 KMDF 调试器扩展，并了解如何在基本调试方案中使用它们。

## <a name="prerequisites"></a>必备条件


这一系列的演示是在高级技术级别提供的。 若要充分利用此内容，你应该了解 Windows 内核调试器（windbg），并熟悉如何使用 KMDF 创建和使用代码。 由于每个会话都是在上一个会话中生成的，因此我们建议你按列出的顺序查看这些演示。

## <a name="video-series-debugging-kernel-mode-driver-framework-drivers"></a>视频系列：调试内核模式驱动程序框架驱动程序


-   [会话1：转储 KMDF 日志（10分钟）](https://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-1.wmv) \[media file\]

    KMDF 日志是一项重要的功能，可帮助快速确定问题的根本原因。 本课程演示如何转储内核调试器中的 KMDF 日志。 它还提供了有关如何更改日志的大小和详细信息的信息，并提供有关扫描日志的一些提示。

-   [会话2：获取有关 KMDF 驱动程序及其对象的信息（15分钟）](https://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-2.wmv) \[media file\]

    KMDF 提供了几个可帮助你浏览有关驱动程序的各种类型信息的调试器命令。 此会话演示如何转储 KMDF 驱动程序创建的所有框架对象，包括父子层次结构、验证程序状态和设备层次结构。 这些命令通常是更深入的调查的起点。

-   [会话3：转储设备和队列（15分钟）](https://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-3.wmv) \[media file\]

    本课程演示如何获取有关 KMDF 设备对象的详细信息，包括即插即用（PnP）和电源状态、电源策略所有权、电源配置、PnP 和电源回拨以及设备属性。 还介绍了如何获取有关开放句柄的信息、如何浏览为该设备配置的所有 i/o 队列，以及如何转储单个请求。

 

 





