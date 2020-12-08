---
title: 测试传感器功能
description: 可以使用传感器诊断工具来测试传感器的功能。
keywords:
- 测试传感器
- 传感器，测试
- 测试传感器功能
- 当前报表间隔
- 更改敏感度
- 传感器事件
- 事件，传感器
- 测试传感器事件
- 测试传感器数据检索
- 测试传感器属性支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2218799e130281d770a4f8c3e3cb6a612ec60fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805063"
---
# <a name="testing-sensor-functionality"></a>测试传感器功能


可以使用传感器诊断工具来测试传感器的功能。 使用该工具可确保驱动程序和固件正确地从设备转发数据，并正确响应来自应用程序的请求。 此外，您可以使用该工具来验证您的驱动程序是否正确支持对当前报表间隔的更改和更改敏感度。
 

传感器平台 (API 和 DDI) 支持事件通知和属性检索。

-   用户可以注册以接收来自设备的 (或通知) 的事件。 驱动程序将这些事件以最严格的订户速率触发到所有订阅服务器。 还可以手动请求数据。 例如，游戏应用程序可以请求每秒20次接收加速感应事件通知，或在驱动程序触发事件时订阅获取更新。
-   有些情况下，应用程序使用属性而不是事件来检索传感器数据。 例如，在人机状态传感器检测到用户的状态之后，控制显示亮度的应用程序可能会选择仅检索当前的光源级别。

有关事件的更完整说明，请参阅更改敏感度 (及其 interrelationship) ，请参阅 [筛选数据](filtering-data.md) 主题。 有关使用传感器诊断工具测试事件处理的信息，请参阅 [测试传感器事件](testing-sensor-events.md) 主题。

有关使用传感器诊断工具来测试属性检索的信息，请参阅 [测试传感器属性](testing-sensor-properties.md) 主题。

## <a name="related-topics"></a>相关主题
[传感器诊断工具](the-sensor-diagnostic-tool.md)  
[测试传感器事件](testing-sensor-events.md)  
[测试传感器属性](testing-sensor-properties.md)  



