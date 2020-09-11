---
title: 指定传感器图标
description: 指定传感器图标
ms.assetid: fe4a204f-befb-45d4-ad95-03b9e788e375
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f67601c94a34edd928fdf8b1ab395e5029502dc
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010467"
---
# <a name="specifying-a-sensor-icon"></a>指定传感器图标


传感器驱动程序可以指定一组平台定义的图标或自定义图标，以表示控制面板中的设备。 若要指定特定的图标，请在驱动程序的 INX (或 INF) 文件中创建一个 DeviceIcon 条目，格式如下：

```c
DeviceIcon,,,,"<full path to DLL>,-<resource id>"
```

例如，若要指定光源传感器图标，请添加以下部分：

```c

[DriverPropertiesSection]
DeviceIcon,,,,"%SystemRoot%\system32\sensorscpl.dll,-1008"
```

若要指定自定义图标，请将 DLL 路径替换为包含图标的 DLL 的路径，并将资源 ID 替换为适当的值。

如果你的 INX 文件尚未包含驱动程序属性部分，则必须将指令添加 `AddProperty` 到 `_Install.NT` 部分。 例如，时间传感器示例可能包括以下部分：

```c

[TimeSensor_Install.NT]
CopyFiles       = UMDriverCopy
AddProperty     = DriverPropertiesSection
```

有关 INF 文件中的设备属性的详细信息，请参阅 [**Inf AddProperty 指令**](../install/inf-addproperty-directive.md)。

## <a name="related-topics"></a>相关主题
[**传感器图标常量**](sensor-icon-constants.md)