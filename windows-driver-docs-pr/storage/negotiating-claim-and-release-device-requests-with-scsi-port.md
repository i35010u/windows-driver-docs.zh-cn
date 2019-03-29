---
title: 通过 SCSI 端口协商声明和释放设备请求
description: 通过 SCSI 端口协商声明和释放设备请求
ms.assetid: 0eb00955-127c-4ef7-a18f-69448b5fd105
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda2be72f5eed52d0a4e255e053a68d265f6f335
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561941"
---
# <a name="negotiating-claim-and-release-device-requests-with-scsi-port"></a>通过 SCSI 端口协商声明和释放设备请求


## <span id="ddk_negotiating_claim_and_release_device_requests_with_scsi_port_kg"></span><span id="DDK_NEGOTIATING_CLAIM_AND_RELEASE_DEVICE_REQUESTS_WITH_SCSI_PORT_KG"></span>


存储类驱动程序必须从 SCSI 端口请求权限*声明*设备。 有关如何类驱动程序声明设备详细信息，请参阅[存储类驱动程序 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

新的设备的发现和枚举的过程根据它们是即插即用设备或预 PnP 存储设备而有所不同。 SCSI 端口驱动程序来试图控制在同一设备的 pre PNP 和即插即用驱动程序之间担当中介。 因此，存储设备驱动程序之前必须获取权限从 SCSI 端口与其设备进行交互。

若要获取使用设备的权限，设备驱动程序将发送索赔请求到 SCSI 端口，通常在其*AddDevice*例程。 索赔请求包含具有 IOCTL 到 I/O 的控制代码的 IRP\_SCSI\_EXECUTE\_NONE 和指向在 SRB **Parameters.Scsi.Srb**。 SRB 是函数类型 SRB\_函数\_声明\_设备。

SCSI 端口维护一个标志，该标志指示设备是否已声明的每台设备。 SCSI 端口设置此标志响应 SRB\_函数\_声明\_设备请求;SCSI 端口清除响应 SRB 标志\_函数\_删除\_设备的请求。

SCSI 端口更高级别的驱动程序尝试声明不存在的设备，如果声明请求 IRP 失败并返回状态的状态\_设备\_DOES\_不\_存在。

SCSI 端口更高级别的驱动程序尝试声明已声明的设备，如果声明请求 IRP 失败并返回状态的状态\_设备\_忙。

如果声明请求成功，SCSI 端口 SRB 数据缓冲区指针中返回设备的当前设备对象。

若要释放先前声明的设备，更高级别的驱动程序必须将版本的设备请求发送到 SCSI 端口驱动程序：版本的设备请求包含与 SRB**函数**值 SRB\_函数\_释放\_设备。

声明的存储类驱动程序的角度从设备请求的讨论，请参阅[存储类驱动程序 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

 

 




