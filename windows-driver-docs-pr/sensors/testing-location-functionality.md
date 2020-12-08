---
title: 测试定位功能
description: 传感器诊断工具包含单独的 "位置" 选项卡，用于记录特定于位置的属性。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d5318f875edebfca215e7019416cf86397cb9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805067"
---
# <a name="testing-location-functionality"></a>测试定位功能


传感器诊断工具包含单独的 "位置" 选项卡，用于记录特定于位置的属性。 这些属性包括纬度、经度和市政地址。

>[!NOTE]
> 传感器诊断工具可用于在 Windows 8.1 及更早版本的操作系统上进行测试。 此工具现在已不推荐用于 Windows 10，因此对于 Windows 10 及更高版本的操作系统上的传感器驱动程序测试和诊断，请使用 Microsoft Store 中的 SensorInfo 应用程序。



## <a name="configuring-the-sensor-diagnostic-tool-to-capture-location-data"></a>配置传感器诊断工具以捕获位置数据


以下过程描述如何配置传感器诊断工具，以便捕获 Windows 位置提供程序的事件。

1.  展开左侧传感器窗格中 Windows 位置提供程序的节点，并选中 " **已连接** " 和 "已 **订阅** " 框。
2.  单击 "Windows 位置提供程序" 节点。

单击节点后，右侧窗格中的 " **属性** " 和 " **数据** " 选项卡将更新为 "位置数据"。

## <a name="tracking-location-data"></a>跟踪位置数据


将传感器诊断工具配置为捕获位置数据之后 (参阅本主题中的上一节) ，你可以使用 " **位置** " 选项卡开始查看特定属性和数据。

1.  打开 " **位置** " 选项卡。
2.  若要查看纬度值和经度值，请在左窗格中单击 "经纬度" 节点。
3.  若要查看市政地址，请在左窗格中单击 "CivicAddress" 节点。

## <a name="related-topics"></a>相关主题
[传感器诊断工具](the-sensor-diagnostic-tool.md) 
[测试传感器功能](testing-sensor-functionality.md)



