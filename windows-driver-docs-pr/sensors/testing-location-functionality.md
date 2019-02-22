---
title: 测试位置的功能
description: 传感器诊断工具包括单独的位置选项卡，以记录特定于位置的属性。
ms.assetid: A96AF9C7-69FA-492C-941E-4E296488875C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8684ac12c530cebc1c25e08f58b5a1e5d9abd5c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547499"
---
# <a name="testing-location-functionality"></a>测试位置的功能


传感器诊断工具包括单独的位置选项卡，以记录特定于位置的属性。 这些属性包括纬度、 经度和市政地址。

>[!NOTE]
> 传感器诊断工具是适用于 Windows 8.1 和更早的操作系统上进行测试。 现在适用于 Windows 10 不推荐使用该工具，因此对于传感器驱动程序测试和诊断在 Windows 10 和更高版本操作系统上的，请使用 SensorInfo 应用从 Microsoft Store。



## <a name="configuring-the-sensor-diagnostic-tool-to-capture-location-data"></a>配置传感器诊断工具，用于捕获位置数据


以下过程介绍如何配置传感器诊断工具以 Windows 位置提供程序捕获的事件。

1.  展开左侧的传感器窗格中的 Windows 位置提供程序的节点并检查**已连接**并**已订阅**框。
2.  单击 Windows 位置提供程序节点。

单击节点后,**属性**并**数据**使用位置数据更新在右窗格中的选项卡。

## <a name="tracking-location-data"></a>跟踪位置数据


配置传感器诊断工具，用于捕获位置数据 （请参阅本主题的上一节） 后，您可以开始使用查看特定的属性和数据**位置**选项卡。

1.  打开**位置**选项卡。
2.  若要查看纬度和经度值，请单击左窗格中的经纬度节点。
3.  若要查看市政地址，请单击左窗格中的指定 CivicAddress 节点。

## <a name="related-topics"></a>相关主题
[传感器诊断工具](the-sensor-diagnostic-tool.md)
[测试传感器功能](testing-sensor-functionality.md)



