---
title: UPnP 设备的容器 ID
description: UPnP 设备的容器 ID
ms.assetid: 29d2ed0e-e746-4f0a-88f3-bd07d5750485
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 668e6638aea1f962424e45ffbb064884dbc1a527
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902605"
---
# <a name="container-ids-for-upnp-devices"></a>UPnP 设备的容器 ID

从 Windows 7 开始，支持 PnP 扩展 (Pnp-id) 和通用 PnP (UPnP) 的设备可以通过在设备说明文档中包含 **X_containerId** XML 元素来指定容器 ID。 有关 UPnP 和 UPnP 设备说明文档的详细信息，请参阅 [Upnp 设备体系结构规范。](https://go.microsoft.com/fwlink/p/?linkid=142402)

**X_containerId** XML 元素声明如下：

```cpp
<df:X_containerId xmlns:df="">
  xs:string
</df:X_containerId>
```

**X_containerId** XML 元素类型是一个字符串，其值是全局唯一标识符 (*GUID*) 。 此字符串的格式为 *{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}*。

下面是 **X_containerId** XML 元素的一个示例。

```cpp
<df:X_containerId xmlns:df="">
  {101392d0-5e91-11dd-ad8b-0800200c9a66}
</df:X_containerId>
```

**X_containerId** XML 元素必须位于 &lt; &gt; "UPnP 设备说明" 文档的 "设备" 部分中。 下面的示例演示设备说明文档中 **X_containerId** 元素的正确位置。

>[!NOTE]
>这不是完整的 UPnP 设备说明文档。 有关 UPnP 的详细信息，请参阅 [Upnp 设备体系结构规范。](https://go.microsoft.com/fwlink/p/?linkid=142402)

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

如果 UPnP 设备说明文档未包括 **X_containerId** XML 元素，则即插即用 (PnP) manager 将通过设备的唯一设备名称 (UDN) 生成一个容器 ID。
