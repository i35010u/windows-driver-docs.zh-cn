---
title: 自动配置详细信息
description: 自动配置详细信息
ms.assetid: ba596ce3-724d-45c4-85ee-2486a31a0c01
keywords:
- 自动配置 WDK 打印机，有关打印机自动配置
- 打印机自动配置 WDK 打印机，有关打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a93005862ccec292fccc41477680bd0af0f073
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575411"
---
# <a name="autoconfiguration-details"></a>自动配置详细信息


自动配置适用于通过之间打印子系统和打印机的打印机的双向通信 （也称为双向通信）。 若要运行的自动配置，必须能够打印机：

-   了解通过端口监视器发送的查询。

-   生成对查询的相应响应。

若要支持自动配置，打印机驱动程序和端口监视器必须进行修改。

打印机驱动程序必须：

-   请注意 bidi 通知架构。

-   可以接收有关设备使用 bidi 通知架构的配置更改的通知。

-   可以要求从打印机使用的配置数据[bidi 通信接口](https://msdn.microsoft.com/library/windows/hardware/ff545163)，并专门 IBidiSpl2 COM 接口。

端口监视器必须：

-   支持设备协议支持的查询打印机的配置。

-   可以从打印机接收未经请求的状态消息。

-   将未经请求的状态消息转换为相应的驱动程序通知。

-   将所有的设备状态和配置数据当前通过轮询或警报。

-   驱动程序或应用程序的设备中的任何配置更改将会通知。

在 Windows Vista 中支持自动配置。 但是，在配置中使用指向并打印，在服务器上的端口监视器和客户端上的驱动程序必须都为支持双向通信。

本部分包含以下主题：

[在设备安装过程中自动配置](autoconfiguration-during-device-installation.md)

[在更改配置的自动配置](autoconfiguration-during-configuration-change.md)

 

 




