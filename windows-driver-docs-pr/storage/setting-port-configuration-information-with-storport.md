---
title: 使用 Storport 设置端口配置信息
description: 使用 Storport 设置端口配置信息
ms.assetid: dcc2cb3c-2fe6-4f70-814b-66b59a237dd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5efbc603506523ec21eb99cef74e757dcb9d2165
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845230"
---
# <a name="setting-port-configuration-information-with-storport"></a>使用 Storport 设置端口配置信息


## <span id="ddk_setting_port_configuration_information_with_storport_kg"></span><span id="DDK_SETTING_PORT_CONFIGURATION_INFORMATION_WITH_STORPORT_KG"></span>


当 Microsoft Windows PnP 管理器发现由 Storport 管理的适配器时，它会通知 Storport 驱动程序启动它。 接下来，Storport 调用微型端口驱动程序的[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)例程，并传入[**端口\_配置\_信息（Storport）** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))结构。

由于 Storport 管理的所有适配器都是 PnP 设备，因此*HwStorFindAdapter*不会以物理方式搜索适配器。 相反，此微型端口驱动程序例程尝试使用端口\_配置\_信息结构中指定的参数初始化适配器，并完成端口\_配置的初始化\_有关信息，请将这些值存储在端口\_配置中\_信息。

有关详细信息，请参阅[**端口\_配置\_信息（SCSI）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)和[**端口\_配置\_信息（STORPORT）** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))。

 

 




