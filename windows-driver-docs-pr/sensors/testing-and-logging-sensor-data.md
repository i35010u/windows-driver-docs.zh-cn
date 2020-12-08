---
title: 测试传感器属性支持
description: 使用传感器诊断工具来测试驱动程序和固件是否支持属性检索。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d68d610b47e8be56bc36199d47afb4d441432ff5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812125"
---
# <a name="testing-sensor-property-support"></a>测试传感器属性支持


使用传感器诊断工具来测试驱动程序和固件是否支持属性检索。 该工具在传感器 API 中调用属性，以确定是否支持属性检索。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-retrieve-sensor-properties"></a>配置传感器诊断工具以检索传感器属性


若要配置诊断工具，以便它可以检索加速感应的属性，请执行以下操作：

1.  在左传感器窗格中展开加速感应的节点，并选中 " **已连接** " 框。
2.  单击左侧传感器窗格中的 "加速感应" 节点。

右窗格的 "属性" 部分包含传感器的更新属性数据。 此数据与设备支持的属性相对应。

[测试传感器事件](testing-sensor-events.md)主题介绍了如何测试驱动程序和固件是否支持更改敏感度和当前报告间隔。 请参阅以下部分，了解如何使用该工具在测试属性支持时更改这些设置。

## <a name="related-topics"></a>相关主题
[测试传感器功能](testing-sensor-functionality.md)  
[测试传感器数据检索](testing-sensor-properties.md)  
[测试传感器事件](testing-sensor-events.md)  



