---
title: 使用 Storport 设置端口配置信息
description: 使用 Storport 设置端口配置信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c2a4fba4f21472c6c57b90f69ed02a0537810e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790357"
---
# <a name="setting-port-configuration-information-with-storport"></a>使用 Storport 设置端口配置信息


## <span id="ddk_setting_port_configuration_information_with_storport_kg"></span><span id="DDK_SETTING_PORT_CONFIGURATION_INFORMATION_WITH_STORPORT_KG"></span>


当 Microsoft Windows PnP 管理器发现由 Storport 管理的适配器时，它会通知 Storport 驱动程序启动它。 接下来，Storport 调用微型端口驱动程序的 [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter) 例程，并 [**传入 \_ \_ (Storport) 结构的端口配置信息**](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)) 。

由于 Storport 管理的所有适配器都是 PnP 设备，因此 *HwStorFindAdapter* 不会以物理方式搜索适配器。 相反，此微型端口驱动程序例程尝试使用端口配置信息结构中指定的参数初始化适配器 \_ \_ ，并完成端口配置信息的初始化 \_ ，并将 \_ 这些值存储在 \_ 设置 \_ 了 Storport 可能需要的端口配置信息中以初始化设备扩展。

有关详细信息，请参阅 [**端口 \_ 配置 \_ 信息 (SCSI)**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) 和 [**端口 \_ 配置 \_ 信息 (STORPORT)**](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))。

 

