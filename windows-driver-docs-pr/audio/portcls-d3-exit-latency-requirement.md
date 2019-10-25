---
title: PortCls D3 退出延迟要求
description: 本主题讨论如何使用 Windows 端口类驱动程序（PortCls）来处理 D3 睡眠状态的退出延迟要求。
ms.assetid: 3CEFF85B-5A2E-4F85-BCAC-00F1773A8F4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0f77ecf7f929fb6056254756b60439d8897f42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832467"
---
# <a name="portcls-d3-exit-latency-requirement"></a>PortCls D3 退出延迟要求


本主题讨论如何使用 Windows 端口类驱动程序（PortCls）来处理 D3 睡眠状态的退出延迟要求。

当系统进入 "完全正常工作" （例如，"睡眠" 或 "连接待机"）以外的平台电源状态时，可能会放松音频适配器返回到 D0 （完全正常）所需的退出延迟。 这使得音频适配器可以使用小于 D3 的睡眠状态，即使这些深状态可能导致更长的退出延迟（退出时间）。

PortCls 现在可以使用新的电源管理接口生成新的 D3 出口延迟，然后将其动态地传达给音频微型端口驱动程序。 这些公差表示为[**PC\_EXIT\_滞后时间**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-_pc_exit_latency)枚举值。

有关新电源管理接口的详细信息，请参阅[ **IAdapterPowerManagement3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement3)

 

 




