---
title: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
description: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
keywords:
- 端口驱动程序 WDK 音频，默认 Dmu 端口驱动程序
- 默认 Dmu 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2459c6857e363d90dea668860299b5558a9bd280
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801041"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>将 PortDMus 设置为默认的 DirectMusic 端口驱动程序


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


若要使 Dmu 端口驱动程序成为所有 DirectMusic 应用程序的默认驱动程序，请使用 uuidgen.exe 或 guidgen.exe 生成 GUID (，这些或包括在 Microsoft Windows SDK) 中，用于唯一标识合成合成。 [**KSPROPERTY \_ 合成 \_ cap**](/previous-versions/ff537389(v=vs.85))属性处理程序应将此 guid 复制到 [**SYNTHCAPS**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)结构的 **GUID** 成员中。 此外，请修改驱动程序的 INF 文件以设置以下注册表项：

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```
