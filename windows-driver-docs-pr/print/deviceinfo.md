---
title: DeviceInfo
description: DeviceInfo
ms.assetid: be2ee9e7-bd94-4f96-8d93-3b6f5fd9350e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764321e1ca7b7524a6c03a66415b104f2db48a37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374543"
---
# <a name="deviceinfo"></a>DeviceInfo


架构路径：\\Printer.DeviceInfo

节点类型： 属性

DeviceInfo 属性包含有关设备作为一个整体的信息。 这种数据可以设置用户/管理员通过进行个性化设置设备。

DeviceInfo 属性包含以下子值。

FriendlyName

制造商

型号名称

Location

备注

FirmwareVersion

IEEE1284DeviceID

[NetworkingInfo](networkinginfo.md)

### <a name="span-idfriendlynamespanspan-idfriendlynamespan-friendlyname"></a><span id="friendlyname"></span><span id="FRIENDLYNAME"></span> FriendlyName

Schema Path:\\Printer.DeviceInfo:FriendlyName

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个用户创建的用户可设置名称，用于标识设备。

### <a name="span-idmanufacturerspanspan-idmanufacturerspan-manufacturer"></a><span id="manufacturer"></span><span id="MANUFACTURER"></span> 制造商

Schema Path:\\Printer.DeviceInfo:Manufacturer

节点类型： 值

数据类型： BIDI\_字符串

说明： 设备制造商的名称。

### <a name="span-idmodelnamespanspan-idmodelnamespan-modelname"></a><span id="modelname"></span><span id="MODELNAME"></span> ModelName

Schema Path:\\Printer.DeviceInfo:ModelName

节点类型： 值

数据类型： BIDI\_字符串

说明： 设备模型，包括型号，但不包括制造商名称的名称。

### <a name="span-idlocationspanspan-idlocationspan-location"></a><span id="location"></span><span id="LOCATION"></span> 位置

架构路径：\\Printer.DeviceInfo:Location

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前设备的位置。

### <a name="span-idcommentspanspan-idcommentspan-comment"></a><span id="comment"></span><span id="COMMENT"></span> 注释

架构路径：\\Printer.DeviceInfo:Comment

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个字符串，包含管理员或设备所在的组织的重要信息。

### <a name="span-idfirmwareversionspanspan-idfirmwareversionspan-firmwareversion"></a><span id="firmwareversion"></span><span id="FIRMWAREVERSION"></span> FirmwareVersion

架构路径：\\Printer.DeviceInfo:FirmwareVersion

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个字符串，其中包含当前的设备的固件版本。

### <a name="span-idieee1284deviceidspanspan-idieee1284deviceidspan-ieee1284deviceid"></a><span id="ieee1284deviceid"></span><span id="IEEE1284DEVICEID"></span> IEEE1284DeviceID

Schema Path:\\Printer.DeviceInfo:IEEE1284DeviceID

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个字符串，其中包含设备的 IEEE 1284 2000年设备 ID。 请注意，必须不能指定长度字段。 值由打印机供应商分配，并且必须未本地化的打印服务。

IEEE 1284 2000年设备 ID 是跟定义外围特征和功能的 ASCII 字符的区分大小写字符串的长度字段。 不能包括长度字节。 设备 ID 序列由一系列密钥和窗体的值组成：

键： 值 {，值}，重复的每个密钥

如所述，每个密钥将具有一个值，可能会有多个值。 制造商和型号，最小所需的密钥 （区分大小写）。 （这些密钥可能缩写为制造业和 MDL 分别。）每个实现必须提供这两个密钥，以及可能的其他的。 每个密钥 （和每个值） 是字符的字符串。 除冒号 （:）、 （、）、 逗号和分号 （;） 的任何字符可以是作为字符串的项 （或值） 的一部分包含在内。 任何前导或尾随空格 (空间\[x '20'\]，选项卡\[x '09'\]，VTAB\["0B"x\]，CR\[x '0 D'\]，NL\["0A"x\]，或 FF\[x '0 C'\]) 在字符串中将忽略分析程序 （但仍计在内作为整体序列的长度的一部分）。

下面的代码示例显示了一个 ID 字符串，它显示了可选命令集、 注释和活动命令设置参数和及其关联的值。

**请注意**  的所有文本必须位于一行上。

 

```cpp
MANUFACTURER:ACME Manufacturing;
MODEL:LaserBeam 9;
COMMAND SET:PCL,PJL,PS,XHTML-Print+xml;
COMMENT:Anything you like;
ACTIVE COMMAND SET:PCL;
```

 

 




