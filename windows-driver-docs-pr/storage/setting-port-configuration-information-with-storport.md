---
title: 使用 Storport 设置端口配置信息
description: 使用 Storport 设置端口配置信息
ms.assetid: dcc2cb3c-2fe6-4f70-814b-66b59a237dd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a45a6fba96058cc2dd24a1400ca7af1ac9609249
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363943"
---
# <a name="setting-port-configuration-information-with-storport"></a>使用 Storport 设置端口配置信息


## <span id="ddk_setting_port_configuration_information_with_storport_kg"></span><span id="DDK_SETTING_PORT_CONFIGURATION_INFORMATION_WITH_STORPORT_KG"></span>


当 Microsoft Windows PnP 管理器发现由 Storport 的适配器时，它将通知 Storport 驱动程序来启动它。 Storport 接下来，调用微型端口驱动程序[ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)例程，并传入[**端口\_配置\_信息 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))结构。

Storport 由管理的所有适配器都是即插即用设备，因为*HwStorFindAdapter*不会以物理方式搜索的适配器。 相反，此微型端口驱动程序例程尝试初始化适配器使用在端口中指定的参数\_配置\_信息结构，并完成端口的初始化\_配置\_信息，将这些值存储在端口\_配置\_Storport 可能需要以初始化设备扩展的信息。

有关详细信息，请参阅[**端口\_配置\_信息 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)并[**端口\_配置\_信息 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))。

 

 




