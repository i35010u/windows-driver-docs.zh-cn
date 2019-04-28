---
title: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
description: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
ms.assetid: 1e498eb1-8a48-4240-8557-2fd2bba02abb
keywords:
- 端口驱动程序 WDK 音频，默认 Dmu 端口驱动程序
- 默认 Dmu 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb7d2a29a7589de2c217b9c8fe14cbeffdb018e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332389"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>将 PortDMus 设置为默认的 DirectMusic 端口驱动程序


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


若要使 Dmu 端口驱动程序的默认值为所有 DirectMusic 应用程序，生成 GUID （使用 uuidgen.exe 或 guidgen.exe，包括在 Microsoft Windows SDK） 来唯一标识你合成器。 你[ **KSPROPERTY\_合成\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff537389)属性处理程序应将复制到此 GUID **Guid**隶属[ **SYNTHCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff538424)结构。 此外，修改驱动程序的 INF 文件以设置以下注册表项：

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```








