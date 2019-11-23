---
title: COPP 状态
description: COPP 状态
ms.assetid: bec8f6b6-17d0-4797-9898-add0629cba4d
keywords:
- 复制保护 WDK COPP，状态
- 视频复制保护 WDK COPP，状态
- COPP WDK DirectX VA，status
- 受保护的视频 WDK COPP，状态
- 状态信息 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26c0c3be928915a0edc074782d057186cddb5f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839036"
---
# <a name="copp-status"></a>COPP 状态


## <span id="ddk_copp_status_gg"></span><span id="DDK_COPP_STATUS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

视频微型端口驱动程序可以在与 DirectX VA COPP 设备关联的物理连接器上收到 COPP 状态请求。

视频微型端口驱动程序的[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数将被传递到包含请求的[**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)结构。 *COPPQueryStatus*将状态写入*pOutput*参数指向的[**DXVA\_COPPStatusOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)结构。 DXVA\_COPPStatusInput 的**guidStatusRequestID**和**StatusData**成员指定状态请求。 根据请求，视频微型端口驱动程序应将状态信息强制转换为指向[**DXVA\_COPPStatusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdata)、 [**DXVA\_COPPStatusDisplayData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)、 [**DXVA\_COPPStatusHDCPKeyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)或[**DXVA\_COPPStatusSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)结构的指针。 然后，视频微型端口驱动程序应将状态信息复制到 DXVA\_COPPStatusOutput 的**COPPStatus**数组成员。

**请注意**   驱动程序必须在 DXVA\_COPPSTATUSDATA、DXVA\_COPPSTATUSDISPLAYDATA、DXVA\_COPPSTATUSHDCPKEYDATA 或 DXVA\_COPPStatusSignalingCmdData 的**rApp**成员中返回一次使用的128位随机数字。 128位随机数是由发送应用程序生成的，在 DXVA\_COPPStatusInput 的**rApp**成员中提供。

 

驱动程序为所指示的请求返回以下状态数据：

-   对于 " **guidStatusRequestID** " 中设置的 DXVA\_COPPQueryProtectionType，在**StatusData**中设置为 "无"，将在运算\_dwData 的**DXVA**成员中返回以下值的有效 COPPStatusData 组合，这些值指示与 COPP 设备关联的物理连接器上的可用保护机制类型：
    -   COPP\_ProtectionType\_未知
    -   COPP\_ProtectionType\_无
    -   COPP\_ProtectionType\_HDCP
    -   COPP\_ProtectionType\_ACP
    -   COPP\_ProtectionType\_CGMSA
-   对于 " **guidStatusRequestID** " 中设置的 DXVA\_COPPQueryConnectorType，在**StatusData**中设置 "未设置"，将在 DwData\_DXVA 的**COPPStatusData**成员中返回以下值之一，用于标识视频会话使用的物理连接器类型：

    -   COPP\_ConnectorType\_未知
    -   COPP\_ConnectorType\_VGA
    -   COPP\_ConnectorType\_SVideo
    -   COPP\_ConnectorType\_CompositeVideo
    -   COPP\_ConnectorType\_ComponentVideo
    -   COPP\_ConnectorType\_DVI
    -   COPP\_ConnectorType\_HDMI
    -   COPP\_ConnectorType\_LVDS
    -   COPP\_ConnectorType\_TMDS
    -   COPP\_ConnectorType\_D\_JPN

    驱动程序还可以将 COPP\_ConnectorType\_Internal （0x80000000）值与前面的某个连接器类型值组合，以指示图形适配器和显示器监视器之间的连接是永久性的，无法从非用户可维护的机箱外进行访问。

-   对于 DXVA\_COPPQueryLocalProtectionLevel 或\_**DXVA COPPQueryGlobalProtectionLevel guidStatusRequestID**中的集，以及**StatusData**中设置的保护类型，将返回 DwData\_DXVA 的**COPPStatusData**成员的保护级别值。 有关可能的保护级别，请参阅[COPP 命令](copp-commands.md)。 DXVA\_COPPQueryLocalProtectionLevel 请求为视频会话返回当前设置的保护级别。 DXVA\_COPPQueryGlobalProtectionLevel 请求为物理连接器返回当前设置的保护级别。

    COPP 状态查询还可能会请求视频微型端口驱动程序检索某些扩展信息。

-   对于**guidStatusRequestID**中设置的 DXVA\_COPPQueryBusData 和**StatusData**中的任何内容，将在 DwData\_DXVA 的**COPPStatusData**成员中返回以下值之一，这些值用于标识图形硬件使用的总线类型：

    -   COPP\_BusType\_未知
    -   COPP\_BusType\_PCI
    -   COPP\_BusType\_PCIX
    -   COPP\_BusType\_PCIExpress
    -   COPP\_BusType\_AGP

    当图形适配器与其他子系统之间的任何命令和状态接口信号在使用公开提供的规范和标准连接器类型的扩展总线上都不可用时，驱动程序只能结合使用 COPP\_BusType\_集成（0x80000000）值和上述总线类型值之一。 内存总线从此定义中排除。

-   对于在**guidStatusRequestID**中设置的 DXVA\_COPPQueryDisplayData，在**StatusData**中未设置任何内容，将返回[**DXVA\_COPPStatusDisplayData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)结构中的信息，该结构描述了通过与 DirectX VA COPP 设备关联的连接器传输的信号的显示模式。

-   对于在**guidStatusRequestID**中设置的 DXVA\_COPPQueryHDCPKeyData，在**StatusData**中未设置任何内容，将返回[**DXVA\_COPPStatusHDCPKeyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)结构中的信息，该结构描述了高带宽数字内容保护（HDCP）关键选择向量（KSV）。

-   对于在**guidStatusRequestID**中设置的 DXVA\_COPPQuerySignaling，在**StatusData**中未设置任何内容，将返回[**DXVA\_COPPStatusSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)结构中的信息，该结构描述了通过与 DirectX VA COPP 设备关联的物理连接器的信号。

    COPP 状态查询还可能会请求视频微型端口驱动程序检索某些扩展信息。

 

 





