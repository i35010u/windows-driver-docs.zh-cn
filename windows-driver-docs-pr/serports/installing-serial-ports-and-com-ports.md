---
title: 安装串行端口和 COM 端口
description: 安装串行端口和 COM 端口
ms.assetid: 9c755dfa-65e5-4ecb-8544-dd63c6b69c8e
keywords:
- WDK 的串行端口
- COM 端口 WDK 串行设备
- 串行驱动程序 WDK、 COM 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cb6e2f5878cb6c8c07e67018956d5f19e19c5ad
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836354"
---
# <a name="installing-serial-ports-and-com-ports"></a>安装串行端口和 COM 端口

适用于大多数设备，端口[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)和串行函数驱动程序提供操作串行端口和 COM 端口所需的功能。 若要安装串行端口和使用这些系统提供的组件的 COM 端口，请执行以下操作：

- 提供与服务的端口指定端口设备安装程序类和串行函数驱动程序的 INF 文件。

- 要将串行端口配置 COM 端口，符合在中定义的要求[配置的 COM 端口](configuration-of-com-ports.md)。

有关安装串行端口和使用的端口设备安装程序类和串行函数驱动程序的 COM 端口的详细信息，请参阅以下主题：

[安装即插串行端口和 COM 端口](installing-plug-and-play-serial-ports-and-com-ports.md)

[安装旧版 COM 端口](installing-legacy-com-ports.md)

如果你执行 COM 端口的自定义安装，您必须遵守中定义的 COM 端口要求[配置的 COM 端口](configuration-of-com-ports.md)。
