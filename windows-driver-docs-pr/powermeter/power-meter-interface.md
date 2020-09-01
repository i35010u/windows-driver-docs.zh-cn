---
title: 功率表接口
description: 功率表接口
ms.assetid: be3ffb33-f1da-403d-b888-378ffd5cac8a
keywords:
- 电源计量和预算 WDK，接口
- 电源指示器接口 WDK
- PMI WDK 电源计量器
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: bee92fbccd93498bf8938906d74e862e44331ef2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189769"
---
# <a name="power-meter-interface"></a>功率表接口


 (PMI) 的电源指示器接口是通过 WDM 驱动程序提供的，该驱动程序从 [Power Manager](../kernel/power-manager.md) 和 [用户模式电源服务](user-mode-power-service.md) 的 power WMI 提供程序组件 (IRP) ， (UMPS) 。

PMI 提供对各种 i/o 控制 (IOCTL) 请求用户模式服务或应用程序颁发的包的支持。 此 IOCTL 接口提供了有关以下各项的信息：

-   电源计量的功能和配置。 这包括采样间隔和电源阈值。

-   电源指示器的功率预算配置。

-   电源指示器的资产信息，如供应商的名称和计量器的序列号。

-   当前的电源级别和预算信息。

PMI 还支持对电源计量事件的通知，例如在达到或超过电源阈值或预算时。

从 PMI 访问的电源计量信息通常是只读的。 但是，根据电源指示器的功能，其预算配置可能具有只读或读/写权限。

有关 PMI IOCTL 接口的详细信息，请参阅 [Pmi IOCTLs](/windows-hardware/drivers/ddi/pmi/index)。

 
**注意**   Windows 7、Windows Server 2008 R2 和更高版本的 Windows 操作系统支持 PMB 基础结构。


