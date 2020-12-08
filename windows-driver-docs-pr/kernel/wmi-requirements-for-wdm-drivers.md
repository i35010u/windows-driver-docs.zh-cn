---
title: WDM 驱动程序的 WMI 要求
description: WDM 驱动程序的 WMI 要求
keywords:
- WMI WDK 内核，WDM 驱动程序
- WDM 驱动程序 WDK WMI
- Irp WDK WMI
- 请求 WDK WMI
- WMI WDK 内核，请求
- 数据访问接口 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab41d134051ed31c2b85c92e10ade89ee04e88bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782643"
---
# <a name="wmi-requirements-for-wdm-drivers"></a>WDM 驱动程序的 WMI 要求





用 WMI 作为 *数据提供程序* 处理 irp 注册的驱动程序。 系统提供的存储端口驱动程序、类驱动程序和 NDIS 协议驱动程序属于此类别。 有关注册为 WMI 数据提供程序的信息，请参阅 [注册为 Wmi 数据提供程序](registering-as-a-wmi-data-provider.md)。

不处理 Irp 的驱动程序应该只是将 WMI 请求转发到驱动程序堆栈中的下一个较低版本的驱动程序。 接下来，下一个较低的驱动程序将向 WMI 注册并代表第一个驱动程序处理 WMI 请求。 例如，SCSI 微型端口驱动程序和 NDIS 微型端口驱动程序可以注册为 WMI 提供程序，并向其相应的类驱动程序提供 WMI 数据。

向类或端口驱动程序提供 WMI 数据的驱动程序必须支持由类或端口驱动程序定义的特定于驱动程序类型的 WMI 接口。 例如，SCSI 微型端口驱动程序必须在 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)结构中将 **WmiDataProvider** 设置为 **TRUE** ，并 \_ 处理 \_ 来自 SCSI 端口驱动程序的 SRB 函数 WMI 请求。

同样，用于定义自定义数据块的面向连接的 NDIS 微型端口驱动程序必须支持 [oid \_ gen \_ 共同 \_ 支持的 \_ guid](../network/oid-gen-co-supported-guids.md); 否则，ndis \_ \_ \_ 会将这些 oid 和状态指示从由

以下部分介绍如何在处理 Irp 的驱动程序中支持 WMI。

 

