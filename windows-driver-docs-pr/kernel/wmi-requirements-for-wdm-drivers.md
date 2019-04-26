---
title: WDM 驱动程序的 WMI 要求
description: WDM 驱动程序的 WMI 要求
ms.assetid: 8290e570-acd9-4047-bd0b-c1c74847f243
keywords:
- WMI WDK 内核，WDM 驱动程序
- WDM 驱动程序 WDK WMI
- Irp WDK WMI
- 请求 WDK WMI
- WMI WDK 内核请求
- 数据提供程序 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e9121c10cd0dd8dcf45da939bc079140575982
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327005"
---
# <a name="wmi-requirements-for-wdm-drivers"></a>WDM 驱动程序的 WMI 要求





处理 Irp 的驱动程序注册为 WMI*数据提供程序*。 系统提供的存储端口驱动程序、 类驱动程序和协议的 NDIS 驱动程序属于此类别。 有关注册为 WMI 数据提供程序的信息，请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

不处理 Irp 的驱动程序应只是 WMI 将请求转发到驱动程序堆栈中的下一步低驱动程序。 下一步低驱动程序然后向 WMI 注册并处理第一个驱动程序的代表 WMI 请求。 例如，SCSI 微型端口驱动程序和 NDIS 微型端口驱动程序可以将注册为 WMI 提供程序并将其相应的类驱动程序的 WMI 数据。

提供 WMI 数据类或端口驱动程序的驱动程序必须支持由类或端口驱动程序定义的特定于驱动程序的类型 WMI 接口。 例如，SCSI 微型端口驱动程序必须设置**WmiDataProvider**到**TRUE**中[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)结构并且处理 SRB\_函数\_从 SCSI 端口驱动程序的 WMI 请求。

同样，面向连接的 NDIS 微型端口驱动程序，用于定义自定义数据块必须支持[OID\_代\_共同\_支持\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff569566); 否则为 NDIS 映射这些 Oid和状态指示返回从 OID\_GEN\_支持\_NDIS 由定义了一些常见和到 NDIS Guid 为已知的列表。

以下部分介绍如何在处理 Irp 的驱动程序中支持 WMI。

 

 




