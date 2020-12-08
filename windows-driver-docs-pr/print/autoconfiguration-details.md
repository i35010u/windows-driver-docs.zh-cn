---
title: 自动配置详细信息
description: 自动配置详细信息
keywords:
- 自动配置 WDK 打印机，关于打印机自动配置
- 打印机自动配置 WDK 打印机，关于打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47faa4a692b11bad96c1381989ad614cf9337638
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836095"
---
# <a name="autoconfiguration-details"></a>自动配置详细信息


自动配置的工作方式是通过双向打印机通信 (也称为打印子系统和打印机之间的双向通信) 。 若要使自动配置正常工作，打印机必须能够：

-   了解端口监视器发送的查询。

-   生成相应的查询响应。

若要支持自动配置，必须修改打印机驱动程序和端口监视器。

打印机驱动程序必须：

-   请注意，双向通知架构。

-   可以使用双向通知架构接收有关设备配置更改的通知。

-   可以使用 [双向通信接口](/windows-hardware/drivers/ddi/_print/index)从打印机请求配置数据，尤其是 IBidiSpl2 COM 接口。

端口监视器必须：

-   支持能够查询打印机配置的设备协议。

-   能够从打印机接收未经请求的状态消息。

-   将未经请求的状态消息转换为相应的驱动程序通知。

-   通过轮询或警报，使所有设备状态和配置数据保持最新状态。

-   通知驱动程序或应用程序中的任何配置更改。

Windows Vista 支持自动配置。 但是，在使用点和打印的配置中，服务器上的端口监视器和客户端上的驱动程序都必须能够进行双向通信。

本节包含下列主题：

[设备安装期间的自动配置](autoconfiguration-during-device-installation.md)

[配置更改期间的自动配置](autoconfiguration-during-configuration-change.md)

 

