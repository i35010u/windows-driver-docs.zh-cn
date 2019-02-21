---
title: WAN 微型端口驱动程序生成参数
description: WAN 微型端口驱动程序生成参数
ms.assetid: 8e494bd2-c499-48bf-8574-7e8df05be4c8
keywords:
- WAN 微型端口驱动程序 WDK 网络、 构建
- WAN 的 CoNDIS 驱动程序 WDK 网络、 构建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1994189dcdeda2bb602c3466418e16fccd510302
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521068"
---
# <a name="wan-miniport-driver-build-parameters"></a>WAN 微型端口驱动程序生成参数





本主题提供了一些信息定义 NDIS 和 WAN 的 CoNDIS 微型端口驱动程序的生成参数。

生成以标识您的驱动程序作为微型端口驱动程序之前将以下行添加到源文件。

```Text
C_DEFINES=/DNDIS_MINIPORT_DRIVER
```

如果你正在编写的支持通过 TAPI 的连接的 NDIS WAN 的微型端口驱动程序，必须将以下行生成标识您的驱动程序支持的 TAPI 版本之前添加到源文件上。

```Text
C_DEFINES=-DNDIS_TAPI_CURRENT_VERSION=0x00010003
```

如果你正在编写的 CoNDIS WAN 的微型端口驱动程序是集成的微型端口呼叫管理器 (MCM) 和支持的 CoNDIS 地址系列类型共同\_地址\_系列\_TAPI\_代理，必须添加以下生成来确定您的驱动程序支持的 TAPI 版本前将源文件的代码行。

```Text
C_DEFINES=-DNDIS_TAPI_CURRENT_VERSION=0x00030000
```

对于 WAN 微型端口驱动程序，包括路径应包含 Ndiswan.h，以及 Ndis.h。

如果 WAN 微型端口驱动程序支持通过 TAPI 建立的连接，该驱动程序还应包括 Ndistapi.h。

 

 





