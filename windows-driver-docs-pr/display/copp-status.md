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
ms.openlocfilehash: 97952cf54dca423a61d49ef2e9b9aae53ae8acfd
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065252"
---
# <a name="copp-status"></a>COPP 状态


## <span id="ddk_copp_status_gg"></span><span id="DDK_COPP_STATUS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

视频微型端口驱动程序可以在与 DirectX VA COPP 设备关联的物理连接器上收到 COPP 状态请求。

视频微型端口驱动程序的 [*COPPQueryStatus*](./coppquerystatus.md) 函数将被传递到包含请求的 [**DXVA \_ COPPStatusInput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput) 结构。 *COPPQueryStatus*将状态写入*pOutput*参数指向的[**DXVA \_ COPPStatusOutput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)结构。 DXVA COPPStatusInput 的 **guidStatusRequestID** 和 **StatusData** 成员 \_ 指定状态请求。 根据请求，视频微型端口驱动程序应将状态信息强制转换为指向 [**DXVA \_ COPPStatusData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdata)、 [**DXVA \_ COPPStatusDisplayData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)、 [**DXVA \_ COPPStatusHDCPKeyData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)或 [**DXVA \_ COPPStatusSignalingCmdData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata) 结构的指针。 然后，视频微型端口驱动程序应将状态信息复制到 DXVA COPPStatusOutput 的 **COPPStatus** 数组成员 \_ 。

**注意**   驱动程序必须返回在 DXVA **rApp** \_ COPPStatusData、DXVA \_ COPPStatusDisplayData、DXVA \_ COPPStatusHDCPKeyData 或 DXVA COPPStatusSignalingCmdData 的 rApp 成员中使用一次的128位随机数字 \_ 。 128位随机数是由发送应用程序生成的，在 DXVA COPPStatusInput 的 **rApp** 成员中提供 \_ 。

 

驱动程序为所指示的请求返回以下状态数据：

-   对于 \_ 在 **guidStatusRequestID** 中设置的 DXVA COPPQueryProtectionType，在 **StatusData**中设置为 nothing，将在运算 dwData 的 **DXVA** 成员中返回以下值的有效 COPPSTATUSDATA 组合 \_ ，这些值指示与 COPP 设备关联的物理连接器上的可用保护机制类型：
    -   COPP \_ ProtectionType \_ 未知
    -   COPP \_ ProtectionType \_ None
    -   COPP \_ ProtectionType \_ HDCP
    -   COPP \_ ProtectionType \_ ACP
    -   COPP \_ ProtectionType \_ CGMSA
-   对于 \_ **guidStatusRequestID** 中设置的 DXVA COPPQueryConnectorType 和 **StatusData**中未设置任何内容， **将在** dwData DXVA 成员中返回以下值之一， \_ 这些值用于标识视频会话使用的物理连接器类型：

    -   COPP \_ ConnectorType \_ 未知
    -   COPP \_ ConnectorType \_ VGA
    -   COPP \_ ConnectorType \_ SVideo
    -   COPP \_ ConnectorType \_ CompositeVideo
    -   COPP \_ ConnectorType \_ ComponentVideo
    -   COPP \_ ConnectorType \_ DVI
    -   COPP \_ ConnectorType \_ HDMI
    -   COPP \_ ConnectorType \_ LVDS
    -   COPP \_ ConnectorType \_ TMDS
    -   COPP \_ ConnectorType \_ D \_ JPN

    驱动程序还可以将 COPP \_ ConnectorType \_ Internal (0x80000000) 值与前面的某个连接器类型值组合在一起，以指示图形适配器和显示器监视器之间的连接是永久性的，无法从非用户可维护的机箱外进行访问。

-   对于 \_ guidStatusRequestID 中设置的 DXVA COPPQueryLocalProtectionLevel 或 DXVA \_ COPPQueryGlobalProtectionLevel 以及**StatusData**中设置的保护类型，将在 dwData DXVA 的**COPPStatusData**成员中返回一个保护级别值**guidStatusRequestID** \_ 。 有关可能的保护级别，请参阅 [COPP 命令](copp-commands.md)。 DXVA \_ COPPQueryLocalProtectionLevel 请求为视频会话返回当前设置的保护级别。 DXVA \_ COPPQueryGlobalProtectionLevel 请求为物理连接器返回当前设置的保护级别。

    COPP 状态查询还可能会请求视频微型端口驱动程序检索某些扩展信息。

-   对于 " \_ **guidStatusRequestID** **" 中**的 "DXVA COPPQueryBusData" 和 " **StatusData**" 中的任何内容，将在 dwData DXVA 成员中返回以下值之一，这些值用于 \_ 标识图形硬件使用的总线类型：

    -   COPP \_ BusType \_ 未知
    -   COPP \_ BusType \_ PCI
    -   COPP \_ BusType \_ PCIX
    -   COPP \_ BusType \_ PCIExpress
    -   COPP \_ BusType \_ AGP

    \_ \_ 当图形适配器与其他子系统之间的任何命令和状态接口信号在使用公开提供的规范和标准连接器类型的扩展总线上都不可用时，驱动程序只能将 COPP BusType 集成 (0x80000000) 值与上述总线类型值之一组合在一起。 内存总线从此定义中排除。

-   对于 \_ **guidStatusRequestID** 中设置的 DXVA COPPQueryDisplayData 和 **StatusData**中未设置任何内容，将返回 [**DXVA \_ COPPStatusDisplayData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata) 结构中的信息，该结构描述通过与 DirectX VA COPP 设备关联的连接器传输的信号的显示模式。

-   对于 \_ **guidStatusRequestID** 中设置的 DXVA COPPQueryHDCPKeyData 和 **StatusData**中未设置任何内容，将返回 [**DXVA \_ COPPStatusHDCPKeyData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata) 结构中的信息，该结构描述) 密钥选择向量 (KSV)  (的高带宽数字内容保护。

-   对于 \_ **guidStatusRequestID** 中设置的 DXVA COPPQuerySignaling 和 **StatusData**中未设置任何内容，将返回 [**DXVA \_ COPPStatusSignalingCmdData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata) 结构中的信息，该结构描述了如何保护通过与 DirectX VA COPP 设备关联的物理连接器的信号。

    COPP 状态查询还可能会请求视频微型端口驱动程序检索某些扩展信息。

 

