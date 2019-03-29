---
title: 测试传感器功能
description: 传感器诊断工具可用于测试您的传感器功能。
ms.assetid: 1AA232D9-D535-4168-926B-4667289EB7DB
keywords:
- 测试传感器
- 传感器测试
- 测试传感器功能
- 当前报告间隔
- 更改敏感度
- 传感器事件
- 事件传感器
- 传感器的测试活动
- 测试的传感器数据检索
- 测试传感器属性支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa0668928bb69ca25f0b033f654da2631f96bca6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565912"
---
# <a name="testing-sensor-functionality"></a>测试传感器功能


传感器诊断工具可用于测试您的传感器功能。 使用该工具以确保驱动程序和固件正确地将数据转发从设备，并从应用程序正确地响应请求。 此外，该工具可用于验证您的驱动程序是否正确支持对当前报告间隔和更改敏感度的更改。
 

传感器平台 （API 和 DDI） 支持事件通知和检索属性。

-   用户可以注册以接收事件 （或通知） 从设备。 该驱动程序将触发这些事件到所有订阅服务器的最严格的订阅服务器的速率。 此外可以手动请求数据。 例如，游戏应用程序可以请求接收加速感应器事件通知 20 次第二个，或订阅以获得更新，只要该驱动程序激发的事件。
-   在其中应用程序将检索通过使用属性而不是事件的传感器数据的情况。 例如，可以选择控制显示器的亮度应用程序后用户存在传感器检测到用户的状态显示仅检索当前的浅级别。

有关事件的更完整说明，更改敏感度 （和它们之间的关系），请参阅[筛选数据](filtering-data.md)主题。 有关使用传感器诊断工具来测试事件处理的信息，请参阅[测试传感器事件](testing-sensor-events.md)主题。

有关使用传感器诊断工具来测试属性检索的信息，请参阅[测试传感器属性](testing-sensor-properties.md)主题。

## <a name="related-topics"></a>相关主题
[传感器诊断工具](the-sensor-diagnostic-tool.md)  
[传感器的测试活动](testing-sensor-events.md)  
[测试传感器属性](testing-sensor-properties.md)  



