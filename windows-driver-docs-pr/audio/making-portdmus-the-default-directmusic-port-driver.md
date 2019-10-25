---
title: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
description: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
ms.assetid: 1e498eb1-8a48-4240-8557-2fd2bba02abb
keywords:
- 端口驱动程序 WDK 音频，默认 Dmu 端口驱动程序
- 默认 Dmu 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f34f667b1f8d01a9474e39f331d0ced0fb303c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830398"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>将 PortDMus 设置为默认的 DirectMusic 端口驱动程序


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


若要使 Dmu 端口驱动程序成为所有 DirectMusic 应用程序的默认值，请生成 GUID （使用在 Microsoft Windows SDK 中包含的 uuidgen.exe 或 guidgen.exe）来唯一地标识合成。 [**KSPROPERTY\_合成\_cap**](https://docs.microsoft.com/previous-versions/ff537389(v=vs.85))属性处理程序应将此 guid 复制到[**SYNTHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)结构的**GUID**成员中。 此外，请修改驱动程序的 INF 文件以设置以下注册表项：

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```








