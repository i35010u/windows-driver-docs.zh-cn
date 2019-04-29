---
title: 调试 KMDF 驱动程序的视频
description: 本主题包含指向演示如何调试内核模式驱动程序框架 (KMDF) 驱动程序的 Kumar Rajeev 通过三个部分的视频系列。
ms.assetid: 62D0F1DA-318F-4989-94C5-968C67F420C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34255e1be2c2fad5f8e8f6241796212514bcb16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362450"
---
# <a name="videos-debugging-kmdf-drivers"></a>视频：调试 KMDF 驱动程序


本主题包含指向演示如何调试内核模式驱动程序框架 (KMDF) 驱动程序的 Kumar Rajeev 通过三个部分的视频系列。

观看视频之后, 将熟悉 KMDF 调试器扩展并知道如何在基本的调试方案中使用它们。

## <a name="prerequisites"></a>先决条件


在高级技术级别提供了这一系列的演示。 若要充分利用此内容应具有 Windows 内核调试器 (windbg.exe) 的应用知识，并应熟悉创建和使用 KMDF 码。 由于每个会话建立在上一基础之上，我们建议按所列顺序查看这些演示。

## <a name="video-series-debugging-kernel-mode-driver-framework-drivers"></a>视频系列：调试 Kernel-mode Driver Framework 驱动程序


-   [会话 1:将日志转储到 KMDF （10 分钟）](http://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-1.wmv) \[媒体文件\]

    KMDF 日志是一项重要功能，可帮助快速确定问题的根本原因。 本课演示如何转储 KMDF 日志内核调试器中。 此外提供了有关如何更改大小和详细级别的日志，并提供有关扫描日志的一些提示。

-   [会话 2:获取有关 KMDF 驱动程序和及其对象 （15 分钟） 的信息](http://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-2.wmv)\[媒体文件\]

    KMDF 提供了多个调试器命令，可帮助您探索各种类型的驱动程序的信息。 此研讨会介绍了如何转储 KMDF 驱动程序，包括父-子层次结构、 验证器状态和设备层次结构创建的所有框架对象。 这些命令通常是更深入地调查的起点。

-   [会话 3:设备和队列 （15 分钟） 转储](http://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-3.wmv)\[媒体文件\]

    本课演示如何获取有关 KMDF 设备对象包括插即用 (PnP) 和电源状态、 电源策略所有权、 电源配置、 即插即用和电源回调和设备属性的详细的信息。 它还演示如何获取有关打开的句柄的信息，请浏览为该设备配置的所有 I/O 队列和转储各个请求。

 

 





