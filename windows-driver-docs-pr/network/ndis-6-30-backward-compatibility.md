---
title: NDIS 6.30 后向兼容性
description: NDIS 6.30 将向后兼容性功能添加到那些适用于 NDIS 6.20 和 NDIS 6.0 驱动程序。
ms.assetid: 71C2BBCF-206A-4C2D-BF9C-C4074FB9276D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73d185f4b116eb7b9a7eb66af2b7a5176664a67d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383605"
---
# <a name="ndis-630-backward-compatibility"></a>NDIS 6.30 后向兼容性


NDIS 6.30 将向后兼容性功能添加到那些适用于 NDIS 6.20 和 NDIS 6.0 驱动程序。 有关 NDIS 6.20 兼容性问题的信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。 有关 NDIS 6.0 兼容性问题的信息，请参阅[NDIS 6.0 向后兼容性](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)。

有关 NDIS 6.30 功能的详细信息，请参阅[简介 NDIS 6.30](introduction-to-ndis-6-30.md)。

## <a name="features-that-are-no-longer-supported"></a>不再受支持的功能


在 Windows 8 和更高版本不支持以下功能：

-   虚拟机不再支持 TCP 烟囱卸载。 但是，仍然支持本机使用。
-   [IPsec 任务卸载版本 1](ipsec-offload-version-1.md)。 支持 IPsec 任务卸载的所有驱动程序应更新为支持[IPsec 任务卸载版本 2](ipsec-offload-version-2.md)。
-   筛选器中间驱动程序。 相反，使用 NDIS 6。*x*筛选器驱动程序接口。 有关筛选器驱动程序的详细信息，请参阅[NDIS 筛选器驱动程序](ndis-filter-drivers.md)。
-   模拟 802.3 802.11 驱动程序。 NDIS 802.11 驱动程序必须支持本机 802.11 接口。 有关本机 802.11 的详细信息，请参阅[本机 802.11 无线 LAN](https://msdn.microsoft.com/library/windows/hardware/ff560689)。
-   NDIS WAN 驱动程序。 NDIS WAN 驱动程序必须移植到 NDIS 6.0 的 CoNDIS WAN 的驱动程序模型。 有关的 CoNDIS WAN 的详细信息，请参阅[WAN 微型端口驱动程序](wan-miniport-drivers.md)。

## <a name="features-that-have-been-removed"></a>已删除的功能


从 Windows 8 及更高版本已删除了以下功能：

-   NDIS 5.x 及更早版本
-   IrDA 微型端口驱动程序
-   NetDMA
-   令牌环 (802.5)

## <a name="other-changes"></a>其他更改


-   附带了 Windows 8 的 TCP/IP 协议驱动程序已更新为 NDIS 6.30。 但是，此更改是相对较小，因此不需要移植您的驱动程序只需为此功能。 TCP/IP 协议驱动程序是使用 NDIS 6.20 和驱动程序堆栈中的早期驱动程序的向后兼容。

 

 





