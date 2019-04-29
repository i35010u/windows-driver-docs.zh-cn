---
title: UPnP 设备的容器 ID
description: UPnP 设备的容器 ID
ms.assetid: 29d2ed0e-e746-4f0a-88f3-bd07d5750485
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab9e222fe45049ba9f563266192954f8c9b27669
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363450"
---
# <a name="container-ids-for-upnp-devices"></a>UPnP 设备的容器 ID


从 Windows 7 开始，支持即插即用扩展 (PNP-X) 和通用即插即用 (UPnP) 的设备可指定一个容器 ID 通过包括**X_containerId**设备说明文档中的 XML 元素。 有关 UPnP 和 UPnP 设备说明文档的详细信息，请参阅[UPnP 设备体系结构规范。](https://go.microsoft.com/fwlink/p/?linkid=142402)

**X_containerId** XML 元素声明，如下所示：

```cpp
<df:X_containerId xmlns:df="">
  xs:string
</df:X_containerId>
```

**X_containerId** XML 元素类型是一个字符串，其值为全局唯一标识符 (*GUID*)。 此字符串的格式设置为 *{xxxxxxxx xxxx-xxxx-xxxx-在左右加上}*。

以下是一种**X_containerId** XML 元素。

```cpp
<df:X_containerId xmlns:df="">
  {101392d0-5e91-11dd-ad8b-0800200c9a66}
</df:X_containerId>
```

**X_containerId** XML 元素必须为处于&lt;设备&gt;UPnP 设备说明文档的部分。 下面的示例显示了正确的位置**X_containerId**设备说明文档中的元素。

**请注意**  这不是完整的 UPnP 设备说明文档。 有关 UPnP 的详细信息，请参阅[UPnP 设备体系结构规范。](https://go.microsoft.com/fwlink/p/?linkid=142402)

 

```cpp
<?xml version="1.0" ?> 
<root 
 xmlns="urn:schemas-upnp-org:device-1-0"
 xmlns:df=
 "http://schemas.microsoft.com/windows/2008/09/devicefoundation">

 <specVersion>
        <major>major version number</major> 
        <minor>minor version number</minor> 
    </specVersion>

    <URLBase>device URL</URLBase> 

    <device>
 <!-- Place device metadata here. See UPnP spec for details.-->
        <df:X_containerID>
 <!--- Place the ContainerID GUID here.--->
 {101392d0-5e91-11dd-ad8b-0800200c9a66}
      </ df:X_containerID >

    </device>
</root>
```

如果 UPnP 设备说明文档不包括**X_containerId** XML 元素，插 (PnP) 管理器生成的容器 ID 通过设备的唯一设备名称 (UDN)。

 

 





