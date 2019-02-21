---
title: 若要移植到 NDIS 6.30 的微型端口驱动程序的更改摘要
description: 若要更新以支持 NDIS 6.30 NDIS 6.x 微型端口驱动程序，您必须修改以下各节中所述。
ms.assetid: 1EA926FE-367E-4A63-A197-60137D679AE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab26f0c713c142310c006e288ebc64699e075c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542581"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-630"></a>若要移植到 NDIS 6.30 的微型端口驱动程序所需的更改的摘要


若要更新以支持 NDIS 6.30 NDIS 6.x 微型端口驱动程序，您必须修改以下各节中所述。

-   [生成环境和测试](#build-environment-and-testing)
-   [移植的一般要求](#general-porting-requirements)
-   [Wi-Fi Direct 微型端口驱动程序](#wi-fi-direct-miniport-drivers)
-   [基于 USB 的 WWAN （移动宽带） 微型端口驱动程序](#usb-based-wwan-mobile-broadband-miniport-drivers)

有关 NDIS 6.30 功能的详细信息，请参阅[简介 NDIS 6.30](introduction-to-ndis-6-30.md)。

## <a name="build-environment-and-testing"></a>生成环境和测试


-   替换为预处理器定义 NDIS60\_微型端口或 NDIS61\_微型端口或 NDIS620\_微型端口与 NDIS630\_微型端口。 有关详细信息，请参阅[编译 NDIS 6.30 驱动程序](compiling-an-ndis-6-30-driver.md)
-   替换为预处理器定义 NDIS60 或 NDIS61 或 NDIS620，如果存在，NDIS630。
    **请注意**  此项仅适用于 NDIS 中间、 协议和筛选器驱动程序。 大多数 NDIS 微型端口驱动程序不需要此预处理器定义。

     

-   在 NDIS 6.30 NDIS 可以调用[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)如果有两个适配器的两次在并行插入到系统中，在同一时间或在系统启动。 请确保测试在此"启动并行"情况下的微型端口驱动程序。

## <a name="general-porting-requirements"></a>移植的一般要求


-   更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_特征结构中所述[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md).
-   对于已更新的 NDIS 6.30 的所有结构，微型端口驱动程序需要更新**标头**使用正确的结构的成员**修订**并**大小**值。 有关详细信息，请参阅[使用 NDIS 6.30 数据结构](using-ndis-6-30-data-structures.md)。
-   所有微型端口驱动程序应实现否-暂停-上的挂起功能。 有关详细信息，请参阅：
    -   [在 NDIS 6.30 电源管理增强功能](power-management-enhancements-in-ndis-6-30.md)
    -   [**NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)
    -   [**NET\_PNP\_EVENT**](https://msdn.microsoft.com/library/windows/hardware/ff568751)
    -   [OID\_PNP\_SET\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)

## <a name="wi-fi-direct-miniport-drivers"></a>Wi-Fi Direct 微型端口驱动程序


期间[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)，Wi-Fi Direct 支持的微型端口驱动程序必须初始化默认 802.11 MAC 实体。 此外必须将错误报告使用其 Wi-Fi Direct 和虚拟的 Wi-fi 功能[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

**请注意**  注册 NDIS 默认 MAC 实体相对应的 NDIS 端口不需要该驱动程序。

 

## <a name="usb-based-wwan-mobile-broadband-miniport-drivers"></a>基于 USB 的 WWAN （移动宽带） 微型端口驱动程序


对于基于 USB 的移动宽带设备，Windows 8 提供的类驱动程序，使用设备符合 MBIM 规范。 此模型称为移动宽带 (MB) 类驱动程序。 但是，类驱动程序不能支持所有公开的 MB 设备的功能。 出于此原因，MB 功能提供了完善的机制，可用于将扩展的类驱动程序功能。 有关详细信息，请参阅[MB 设备服务](mb-device-services.md)。

如果基于 USB 的 WWAN 微型端口驱动程序不能实现 MB 类驱动程序，它至少必须实现[NDIS 选择性挂起](ndis-selective-suspend.md)功能。

 

 





