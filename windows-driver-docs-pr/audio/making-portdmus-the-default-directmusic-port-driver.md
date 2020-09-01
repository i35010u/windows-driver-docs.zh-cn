---
title: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
description: 将 PortDMus 设置为默认的 DirectMusic 端口驱动程序
ms.assetid: 1e498eb1-8a48-4240-8557-2fd2bba02abb
keywords:
- 端口驱动程序 WDK 音频，默认 Dmu 端口驱动程序
- 默认 Dmu 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b98c77fd1da064aa1c2dbb70dfe1fd72798705c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211430"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>将 PortDMus 设置为默认的 DirectMusic 端口驱动程序


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


若要使 Dmu 端口驱动程序成为所有 DirectMusic 应用程序的默认驱动程序，请使用 uuidgen.exe 或 guidgen.exe 生成 GUID (，这些或包括在 Microsoft Windows SDK) 中，用于唯一标识合成合成。 [**KSPROPERTY \_ 合成 \_ cap**](/previous-versions/ff537389(v=vs.85))属性处理程序应将此 guid 复制到[**SYNTHCAPS**](/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)结构的**GUID**成员中。 此外，请修改驱动程序的 INF 文件以设置以下注册表项：

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```