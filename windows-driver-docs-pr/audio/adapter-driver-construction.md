---
title: 适配器驱动程序构造
description: 适配器驱动程序构造
keywords:
- 音频微型端口驱动程序 WDK，适配器驱动程序
- 微型端口驱动程序 WDK 音频，适配器驱动程序
- 适配器驱动程序 WDK 音频，微型端口驱动程序
- 内核模式驱动程序服务 WDK 音频
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，适配器驱动程序
- 音频适配器 WDK
- 音频适配器 WDK，构造
- 适配器驱动程序 WDK 音频，构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0902b71e07d5b7a140bfe561bef05b2e25600b3f
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757864"
---
# <a name="adapter-driver-construction"></a>适配器驱动程序构造


## <span id="adapter_driver_construction"></span><span id="ADAPTER_DRIVER_CONSTRUCTION"></span>


特定音频适配器卡的驱动程序支持采用适配器驱动程序的形式。 适配器驱动程序由以下内容组成：

-   常规适配器代码，用于执行驱动程序启动和初始化，并实现对适配器卡上所有音频功能通用的任何操作。

-   一组用于管理适配器卡上的特定音频功能的微型端口驱动程序。

硬件供应商为系统未提供的任何微型端口驱动程序提供常规适配器代码和代码。

有关常规适配器代码的示例，请参阅 Sysvad 示例驱动程序中的 **CAdapterCommon** 接口的实现，这将在 [示例音频驱动程序](sample-audio-drivers.md)中讨论。

通过使用分层方法，供应商可以编写一个在多个级别上操作的适配器驱动程序，具体取决于适配器的硬件功能。 确定给定硬件函数所需的支持级别时，供应商应该首先确定系统提供的微型端口驱动程序是否已存在支持函数的 (参阅) 的系统提供的微端口驱动程序的 [**PcNewMiniport**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport) 函数列表。 如果不是，则供应商必须实现专用微型端口驱动程序，但仍可以使用系统提供的端口驱动程序之一 (参阅 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport) 函数的系统提供的端口驱动程序的列表) 。

若要为设备实现 WDM 支持，请执行以下步骤：

1.  如果系统提供的微型端口驱动程序已支持硬件功能，请使用现有的微型端口驱动程序来管理该函数。

2.  如果硬件功能与系统提供的微型端口驱动程序不兼容，则确定该函数是否与至少一个系统提供的端口驱动程序兼容。 如果系统提供的端口驱动程序支持硬件功能，请编写用于管理该函数的微型端口驱动程序部分。 该微型端口驱动程序应遵守所属端口驱动程序所需的微型端口接口的规范。

3.  如果系统提供的端口驱动程序不支持该硬件功能，请编写微型驱动程序来支持该功能。 微型驱动程序应符合流式处理类驱动程序的接口规范。

本部分介绍以下主题：

[启动顺序](startup-sequence.md)

[创建子设备](subdevice-creation.md)

 

