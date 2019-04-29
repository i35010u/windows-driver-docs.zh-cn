---
title: COPP 状态
description: COPP 状态
ms.assetid: bec8f6b6-17d0-4797-9898-add0629cba4d
keywords:
- 复制保护 WDK COPP，状态
- 视频复制保护 WDK COPP，状态
- COPP WDK DirectX va，因此状态
- 受保护视频 WDK COPP 状态
- WDK COPP 的状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7ed0577badd301771c48cea049895a5f9f751c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323795"
---
# <a name="copp-status"></a>COPP 状态


## <span id="ddk_copp_status_gg"></span><span id="DDK_COPP_STATUS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

微型端口驱动程序可以接收 COPP 上的状态与 DirectX VA COPP 设备相关联的物理连接器的请求。

微型端口驱动程序[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)函数传递一个指向[ **DXVA\_COPPStatusInput** ](https://msdn.microsoft.com/library/windows/hardware/ff563899)包含请求的结构。 *COPPQueryStatus*写入到的状态[ **DXVA\_COPPStatusOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff563903)向其结构*pOutput*参数所指向。 **GuidStatusRequestID**并**StatusData** DXVA 成员\_COPPStatusInput 指定状态请求。 微型端口驱动程序应具体取决于该请求，强制转换为指针的状态信息[ **DXVA\_COPPStatusData**](https://msdn.microsoft.com/library/windows/hardware/ff563154)， [ **DXVA\_COPPStatusDisplayData**](https://msdn.microsoft.com/library/windows/hardware/ff563157)， [ **DXVA\_COPPStatusHDCPKeyData**](https://msdn.microsoft.com/library/windows/hardware/ff563896)，或[ **DXVA\_COPPStatusSignalingCmdData** ](https://msdn.microsoft.com/library/windows/hardware/ff563905)结构。 微型端口驱动程序然后应将复制到的状态信息**COPPStatus** DXVA 数组成员\_COPPStatusOutput。

**请注意**  驱动程序必须返回中使用一次为 128 位随机数字**rApp** DXVA 成员\_COPPStatusData、 DXVA\_COPPStatusDisplayData、 DXVA\_COPPStatusHDCPKeyData 或 DXVA\_COPPStatusSignalingCmdData。 128 位随机数字生成由发送应用程序和中未提供**rApp** DXVA 成员\_COPPStatusInput。

 

驱动程序返回指示请求的以下状态数据：

-   为 DXVA\_COPPQueryProtectionType 中设置**guidStatusRequestID** ，并执行任何操作中设置**StatusData**，将返回以下值中的有效或运算组合**dwData** DXVA 成员\_COPPStatusData 指示保护机制与 COPP 设备相关联的物理连接器上的可用类型：
    -   COPP\_ProtectionType\_Unknown
    -   COPP\_ProtectionType\_None
    -   COPP\_ProtectionType\_HDCP
    -   COPP\_ProtectionType\_ACP
    -   COPP\_ProtectionType\_CGMSA
-   为 DXVA\_中设置 COPPQueryConnectorType **guidStatusRequestID** ，并执行任何操作中设置**StatusData**，返回以下值之一中**dwData**DXVA 成员\_COPPStatusData 标识视频会话使用的物理连接器类型：

    -   COPP\_ConnectorType\_Unknown
    -   COPP\_ConnectorType\_VGA
    -   COPP\_ConnectorType\_SVideo
    -   COPP\_ConnectorType\_CompositeVideo
    -   COPP\_ConnectorType\_ComponentVideo
    -   COPP\_ConnectorType\_DVI
    -   COPP\_ConnectorType\_HDMI
    -   COPP\_ConnectorType\_LVDS
    -   COPP\_ConnectorType\_TMDS
    -   COPP\_ConnectorType\_D\_JPN

    该驱动程序也可以组合 COPP\_ConnectorType\_内部 (0x80000000) 值，该值具有一个以上的连接器类型值，以指示图形适配器和监视器之间的连接是永久性的而不从非用户可用的主机箱的外部可访问。

-   为 DXVA\_COPPQueryLocalProtectionLevel 或 DXVA\_COPPQueryGlobalProtectionLevel 集中**guidStatusRequestID**并保护类型中设置**StatusData**，返回中的保护级别值**dwData** DXVA 成员\_COPPStatusData。 对于可能的保护级别，请参阅[COPP 命令](copp-commands.md)。 DXVA\_COPPQueryLocalProtectionLevel 请求将返回当前设置保护级别的视频课程。 DXVA\_COPPQueryGlobalProtectionLevel 请求将返回当前设置物理连接器的保护级别。

    COPP 状态查询还可能会请求微型端口驱动程序检索某些扩展的信息。

-   有关 DXVA\_COPPQueryBusData 中设置**guidStatusRequestID**并在中为 nothing **StatusData**，返回以下值之一中**dwData**的成员DXVA\_COPPStatusData 标识使用的图形硬件的总线类型：

    -   COPP\_BusType\_Unknown
    -   COPP\_BusType\_PCI
    -   COPP\_BusType\_PCIX
    -   COPP\_BusType\_PCIExpress
    -   COPP\_BusType\_AGP

    该驱动程序只能合并 COPP\_BusType\_时没有图形适配器和其他子系统之间的命令和状态接口信号与前面的总线类型值中的一个集成 (0x80000000) 值在使用公开提供的规范和标准连接器类型的扩展总线上可用。 内存总线不在此定义。

-   为 DXVA\_中设置 COPPQueryDisplayData **guidStatusRequestID** ，并执行任何操作中设置**StatusData**中, 返回信息[ **DXVA\_COPPStatusDisplayData** ](https://msdn.microsoft.com/library/windows/hardware/ff563157)结构，描述在与 DirectX VA COPP 设备相关联的连接器上传输的信号的显示模式。

-   为 DXVA\_中设置 COPPQueryHDCPKeyData **guidStatusRequestID** ，并执行任何操作中设置**StatusData**中, 返回信息[ **DXVA\_COPPStatusHDCPKeyData** ](https://msdn.microsoft.com/library/windows/hardware/ff563896)介绍高带宽数字内容保护 (HDCP) 键选择矢量 (KSV) 的结构。

-   为 DXVA\_中设置 COPPQuerySignaling **guidStatusRequestID** ，并执行任何操作中设置**StatusData**中, 返回信息[ **DXVA\_COPPStatusSignalingCmdData** ](https://msdn.microsoft.com/library/windows/hardware/ff563905)结构，它介绍了如何保护与 DirectX VA COPP 设备相关联的物理连接器将经历的信号。

    COPP 状态查询还可能会请求微型端口驱动程序检索某些扩展的信息。

 

 





