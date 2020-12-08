---
title: WAN 微型端口驱动程序生成参数
description: WAN 微型端口驱动程序生成参数
keywords:
- WAN 微型端口驱动程序 WDK 网络，构建
- CoNDIS WAN 驱动程序 WDK 网络，构建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d68eb6f233e9fd88fba0c38445b73bff55804772
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822781"
---
# <a name="wan-miniport-driver-build-parameters"></a>WAN 微型端口驱动程序生成参数





本主题提供了一些有关定义 NDIS 和 CoNDIS WAN 微型端口驱动程序的生成参数的信息。

在生成之前，将以下行添加到源文件，以将你的驱动程序标识为微型端口驱动程序。

```Text
C_DEFINES=/DNDIS_MINIPORT_DRIVER
```

如果要编写支持通过 TAPI 连接的 NDIS WAN 微型端口驱动程序，则必须在生成之前将以下行添加到源文件中，以确定驱动程序支持的 TAPI 版本。

```Text
C_DEFINES=-DNDIS_TAPI_CURRENT_VERSION=0x00010003
```

如果你正在编写一个 CoNDIS WAN 微型端口驱动程序，该驱动程序是集成的微型端口调用管理器 (MCM) 并且支持 CoNDIS address 系列类型的 CO \_ address \_ 系列 \_ TAPI \_ 代理，则必须在生成之前将以下行添加到源文件，以确定驱动程序支持的 TAPI 版本。

```Text
C_DEFINES=-DNDIS_TAPI_CURRENT_VERSION=0x00030000
```

对于 WAN 微型端口驱动程序，包含路径应包括 Ndiswan 以及 Ndis。

如果 WAN 微型端口驱动程序支持通过 TAPI 的连接，则驱动程序还应包括 Ndistapi。

 

 





