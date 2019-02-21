---
title: 协商声明和使用 Storport 发布设备请求
description: 协商声明和使用 Storport 发布设备请求
ms.assetid: 9212f2b0-6319-47a6-8c61-02002ad81178
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fe5d55df4b7d5d70b0bd3b3f266494803c9439c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524325"
---
# <a name="negotiating-claim-and-release-device-requests-with-storport"></a>协商声明和使用 Storport 发布设备请求


存储类驱动程序必须请求权限从到 Storport*声明*设备。 有关如何类驱动程序声明设备详细信息，请参阅[存储类驱动程序 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

新的设备的发现和枚举的过程根据它们是即插即用设备或预 PnP 存储设备而有所不同。 Storport 驱动程序来试图控制在同一设备的 pre PNP 和即插即用驱动程序之间担当中介。 因此，存储设备驱动程序之前必须获取权限从 Storport 与其设备进行交互。 此外，问题的设备可能 HBA 本身或附加到受 HBA 的目标的 LUN。 但是，当指时占用的存储类驱动程序的设备，它始终是正在声明的 LUN 不 HBA。

若要获取使用设备的权限，设备驱动程序将索赔请求发送到 Storport 中。 索赔请求包含具有 IOCTL 到 I/O 的控制代码的 IRP\_SCSI\_EXECUTE\_NONE 和指向在 SRB **Parameters.Scsi.Srb**。 SRB 是函数类型 SRB\_函数\_声明\_设备。

Storport 维护一个标志，该标志指示设备是否已声明的每台设备。 Storport SRB 到响应中设置此标志\_函数\_声明\_设备请求;Storport 清除响应 SRB 标志\_函数\_删除\_设备的请求。

如果更高级别的驱动程序尝试声明不存在的设备，Storport 声明请求 IRP 失败并返回状态的状态\_设备\_DOES\_不\_存在。

如果更高级别的驱动程序尝试声明已声明的设备，Storport 声明请求 IRP 失败并返回状态的状态\_设备\_忙。

如果声明请求成功，Storport SRB 数据缓冲区指针中返回设备的当前设备对象。

若要释放先前声明的设备，更高级别的驱动程序必须将版本的设备请求发送到 Storport 驱动程序：版本的设备请求包含与 SRB**函数**值 SRB\_函数\_释放\_设备。

声明的存储类驱动程序的角度从设备请求的讨论，请参阅[存储类驱动程序 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

 

 




