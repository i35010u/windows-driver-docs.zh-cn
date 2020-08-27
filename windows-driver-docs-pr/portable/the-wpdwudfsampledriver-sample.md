---
description: WpdWudfSampleDriver 示例
title: WpdWudfSampleDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a58563143c7c0eb4cf6eaec1100a9797a12394b5
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969492"
---
# <a name="the-wpdwudfsampledriver-sample"></a>WpdWudfSampleDriver 示例


WPD 驱动程序文档中的此部分介绍了 Windows 驱动程序工具包附带的综合性示例驱动程序 WpdWudfSampleDriver (WDK) 。

综合性 WPD 示例驱动程序 (WpdWudfSampleDriver) 演示 Microsoft Windows 可移植 Devides (WPD) 设备驱动程序接口 (DDI) 的所有方面。 此驱动程序作为普通用户模式驱动程序框架构建， (UMDF) 驱动程序，同时还处理 WPD 命令集。 尽管此驱动程序与实际硬件不交互，但它模拟与支持电话联系人、图片、音乐和视频的设备通信。

此驱动程序是以最简单的方式编写的，旨在演示概念。 因此，示例驱动程序可能会执行操作，或以在生产驱动程序中效率低下的方式进行结构化。 此外，此示例不使用实际硬件。 相反，它将使用内存中的数据结构来模拟设备。 因此，该驱动程序的实现方式对于生产硬件不切实际。

WpdWudfSampleDriver 完成的某些任务是为高级 Windows 便携式设备编写的， (WPD) 驱动程序开发人员。 本部分后面的主题中介绍了这些任务。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





