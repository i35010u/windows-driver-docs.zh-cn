---
title: 指定一个传感器图标
description: 指定一个传感器图标
ms.assetid: fe4a204f-befb-45d4-ad95-03b9e788e375
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b092fc0bbd75c7f4ba4cf037b7b98bb984c619af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378571"
---
# <a name="specifying-a-sensor-icon"></a>指定一个传感器图标


传感器驱动程序可以指定一个平台定义的图标或自定义图标，以表示在控制面板中的设备的一组。 若要指定一个特定的图标，并采用以下格式创建 DeviceIcon 条目在您的驱动程序 INX （或 INF） 文件：

```c
DeviceIcon,,,,"<full path to DLL>,-<resource id>"
```

例如，若要指定光线传感器图标，则要添加以下部分：

```c

[DriverPropertiesSection]
DeviceIcon,,,,"%SystemRoot%\system32\sensorscpl.dll,-1008"
```

若要指定自定义图标，DLL 路径替换为包含您的图标的 DLL 的路径和资源 ID 替换为适当的值。

如果 INX 文件尚未包含驱动程序属性部分，您必须添加`AddProperty`指令`_Install.NT`部分。 例如，时间传感器示例可能包括以下部分：

```c

[TimeSensor_Install.NT]
CopyFiles       = UMDriverCopy
AddProperty     = DriverPropertiesSection
```

INF 文件中的设备属性的详细信息，请参阅[ **INF AddProperty 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)。

## <a name="related-topics"></a>相关主题
[**传感器图标常量**](sensor-icon-constants.md)



