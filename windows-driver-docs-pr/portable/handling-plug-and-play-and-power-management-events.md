---
Description: Handling Plug and Play and Power Management Events
title: 处理插和电源管理事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a09183eaaf9abfbf74a838c93d17f440f1f43ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522715"
---
# <a name="handling-plug-and-play-and-power-management-events"></a>处理插和电源管理事件


Plug and Play (PnP) 或电源管理 (PM) 事件发生时，用户模式驱动程序框架 (UMDF) CDevice 类来处理该事件中调用一个或多个方法。 (在文件中定义 CDevice 类*Device.cpp*。)事件处理程序位于三个接口：**IPnpCallback**， **IPnpCallbackHardware**，和**IPnpCallbackSelfManagedIo**。

在 WpdHelloWorldDriver 示例中，大多数即插即用和 PM 事件处理程序返回任何值或 S\_确定。 有两种例外情况：**IPnpCallbackHardware::OnPrepareHardware**并**IPnPCallbackHardware::OnReleaseHardware**。 下表介绍每种方法。

|                                             |                                                                                                                           |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **IPnpCallbackHardware::OnPrepareHardware** | 调用**WpdBaseDriver::Initialize**方法。 初始化 WPD 类扩展和更新设备的友好名称。 |
| **IPnPCallbackHardware::OnReleaseHardware** | 调用**WpdBaseDriver::Uninitialize**方法和取消初始化 WPD 类扩展。                               |

 

每个接口和其方法的说明，请参阅[UMDF 文档](https://go.microsoft.com/fwlink/p/?linkid=153678)...

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





