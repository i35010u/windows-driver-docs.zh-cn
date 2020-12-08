---
title: DeviceInfo
description: DeviceInfo
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b61414c8ed3a52df893cbd53902d6020bac7c93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797229"
---
# <a name="deviceinfo"></a>DeviceInfo


架构路径： \\ DeviceInfo

节点类型：属性

DeviceInfo 属性包含整个设备的相关信息。 用户/管理员可以设置很多数据来个性化设备。

DeviceInfo 属性包含以下子值。

FriendlyName

制造商

ModelName

位置

评论

FirmwareVersion

IEEE1284DeviceID

[NetworkingInfo](networkinginfo.md)

### <a name="span-idfriendlynamespanspan-idfriendlynamespan-friendlyname"></a><span id="friendlyname"></span><span id="FRIENDLYNAME"></span> 友好

架构路径： \\ DeviceInfo： FriendlyName

节点类型：值

数据类型：双向 \_ 字符串

说明：标识设备的用户创建的用户可设置名称。

### <a name="span-idmanufacturerspanspan-idmanufacturerspan-manufacturer"></a><span id="manufacturer"></span><span id="MANUFACTURER"></span> 提供

架构路径： \\ DeviceInfo：制造商

节点类型：值

数据类型：双向 \_ 字符串

说明：设备制造商的名称。

### <a name="span-idmodelnamespanspan-idmodelnamespan-modelname"></a><span id="modelname"></span><span id="MODELNAME"></span> ModelName

架构路径： \\ DeviceInfo： ModelName

节点类型：值

数据类型：双向 \_ 字符串

说明：设备模型的名称，包括型号，但不包括制造商名称。

### <a name="span-idlocationspanspan-idlocationspan-location"></a><span id="location"></span><span id="LOCATION"></span> 位置

架构路径： \\ DeviceInfo： Location

节点类型：值

数据类型：双向 \_ 字符串

说明：设备的当前位置。

### <a name="span-idcommentspanspan-idcommentspan-comment"></a><span id="comment"></span><span id="COMMENT"></span> 注释

架构路径： \\ DeviceInfo： Comment

节点类型：值

数据类型：双向 \_ 字符串

说明：包含设备所在的管理员或组织的重要信息的字符串。

### <a name="span-idfirmwareversionspanspan-idfirmwareversionspan-firmwareversion"></a><span id="firmwareversion"></span><span id="FIRMWAREVERSION"></span> FirmwareVersion

架构路径： \\ DeviceInfo： FirmwareVersion

节点类型：值

数据类型：双向 \_ 字符串

说明：包含当前设备固件版本的字符串。

### <a name="span-idieee1284deviceidspanspan-idieee1284deviceidspan-ieee1284deviceid"></a><span id="ieee1284deviceid"></span><span id="IEEE1284DEVICEID"></span> IEEE1284DeviceID

架构路径： \\ DeviceInfo： IEEE1284DeviceID

节点类型：值

数据类型：双向 \_ 字符串

说明：包含设备的 IEEE 1284-2000 设备 ID 的字符串。 请注意，不能指定长度字段。 该值由打印机供应商分配，不能通过打印服务进行本地化。

IEEE 1284-2000 设备 ID 是长度字段，后跟一串区分大小写的 ASCII 字符，用于定义外围设备特征和功能。 不得包括长度字节。 设备 ID 序列由一系列格式的键和值组成：

键：值 {，value}，为每个键重复

如上所述，每个键都有一个值，并且可能有多个值。 必需的最小密钥 (区分大小写) 为制造商和型号。  (这些密钥可能分别缩写为制造和 MDL。 ) 每个实现必须提供这两个密钥，可能还有其他。 每个键 (，) 的每个值都是一个字符串。 除冒号之外的任何字符 (： ) 、逗号 (、) 和分号 (; ) 可以作为键 (或值) 字符串的一部分包括在内。 \[分析程序 (忽略字符串中 (space x "20" \] 、TAB \[ x "09" \] 、VTAB \[ x'0B " \] 、CR \[ X'0D" \] 、NL \[ x'0A "或 FF x'0C") 的任何前导或尾随空格， \] \[ \] 但仍会将其计为序列) 的总长度的一部分。

下面的代码示例显示了一个 ID 字符串，其中显示了可选命令集、注释和活动命令集键及其关联值。

**注意**   所有文本都必须在一行上。

 

```cpp
MANUFACTURER:ACME Manufacturing;
MODEL:LaserBeam 9;
COMMAND SET:PCL,PJL,PS,XHTML-Print+xml;
COMMENT:Anything you like;
ACTIVE COMMAND SET:PCL;
```

 

 




