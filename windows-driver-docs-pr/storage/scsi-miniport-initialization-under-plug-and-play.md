---
title: 在即插即用下进行的 SCSI 微型端口初始化
description: 在即插即用下进行的 SCSI 微型端口初始化
ms.assetid: bf2f9809-8271-4f0f-a2c4-25127fe9c4aa
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- 初始化 SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c3eac06cffafee1101168a74eb86a21c053e02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575636"
---
# <a name="scsi-miniport-initialization-under-plug-and-play"></a>在即插即用下进行的 SCSI 微型端口初始化


## <span id="ddk_scsi_miniport_initialization_under_plug_and_play_kg"></span><span id="DDK_SCSI_MINIPORT_INITIALIZATION_UNDER_PLUG_AND_PLAY_KG"></span>


Windows 2000 和更高版本，旧的微型端口驱动程序是在完全相同的方式与 Microsoft Windows NT 4.0 中初始化。 当旧的微型端口驱动程序调用[ **ScsiPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff564645)，端口驱动程序调用微型端口驱动程序，以查找并初始化其 HBA。 这是其在每个 HBA 找到 （如果 HBA 上的可枚举的总线上） 或重复直到微型端口驱动程序报告它找不到任何更多的设备。 随后控制返回到微型端口驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)例程，其中微型端口驱动程序可以调用**ScsiPortInitialize**再次为其他类型的 HBA （适用于示例中，使用不同的接口或不同的供应商和产品 ID）。 微型端口驱动程序的上下文中进行的所有初始化调用**DriverEntry**例程并按顺序进行的**ScsiPortInitialize**调用。 旧式驱动程序的初始化发生在系统启动时以及在任何其他时间。

在插即用设备，不能保留的初始化顺序。 当为插调用启用微型端口驱动程序**ScsiPortInitialize**，端口驱动程序存储初始化数据以供将来参考，则将返回状态\_成功。 这是与微型端口驱动程序中列出的每个接口类型**PnPInterface**注册表项--任何接口*不*该注册表项中列出仍立即初始化。

更高版本，当插管理器检测到的微型端口驱动程序的 HBA，它将通知端口驱动程序。 端口驱动程序分配必要的系统资源 （如为微型端口驱动程序的设备扩展的内存） 并调用要查找 HBA 的微型端口驱动程序，然后对其进行初始化。 这通常发生在系统启动，但它也可能会发生时系统检测到停靠操作或 CardBus 如 HBA 是热的插入到系统中。

插管理器报告设备时，它具有已分配总线资源 （如 I/O 端口、 内存地址和中断） 为该设备*和该设备仅*。 这些资源提供给微型端口驱动程序，它必须使用这些资源或报告，未找到设备。 具体而言，微型端口驱动程序必须尝试访问端口或指定为找到的设备以外的内存位置。

微型端口驱动程序，如插驱动程序可能会需要检测 nonenumerable 总线上的设备已启动。 这包括总线 ISA，如需要，微型端口驱动程序问题的命令总线上查找其 HBA。 设备位于在这种检测过程记录在注册表中，并初始化为插设备在下次启动系统。

有关插的详细信息，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

 

 




