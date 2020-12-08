---
title: 安装串行端口和 COM 端口
description: 安装串行端口和 COM 端口
keywords:
- 串行端口 WDK
- COM 端口 WDK 串行设备
- 串行驱动程序 WDK，COM 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa45effec837db212a312813b9bc4beba489dee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812005"
---
# <a name="installing-serial-ports-and-com-ports"></a>安装串行端口和 COM 端口

对于大多数设备，端口 [设备安装程序类](../install/overview-of-device-setup-classes.md) 和串行函数驱动程序都提供操作串行端口和 COM 端口所需的功能。 若要使用这些系统提供的组件安装串行端口和 COM 端口，请执行以下操作：

- 提供一个 INF 文件，该文件指定端口设备安装程序类和串行函数驱动程序作为端口的服务。

- 若要将串行端口配置为 COM 端口，请遵守 [Com 端口配置](configuration-of-com-ports.md)中定义的要求。

有关使用端口设备安装程序类和串行函数驱动程序安装串行端口和 COM 端口的详细信息，请参阅以下主题：

[安装即插即用串行端口和 COM 端口](installing-plug-and-play-serial-ports-and-com-ports.md)

[安装旧版 COM 端口](installing-legacy-com-ports.md)

如果对 COM 端口进行自定义安装，则必须遵守 [com 端口配置](configuration-of-com-ports.md)中定义的 com 端口要求。
