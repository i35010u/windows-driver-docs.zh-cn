---
title: IDE 端口驱动程序
description: IDE 端口驱动程序
ms.assetid: 8e292680-6fa7-4f6b-b4ec-6f0f0d795d03
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efa9dacd5faa39a346baac25e80b70ac8a7fcded
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383069"
---
# <a name="ide-port-driver"></a>IDE 端口驱动程序
**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。

在 Microsoft Windows NT 4.0 中，具有 IDE 总线相关联的端口/微型端口驱动程序对是 SCSI 微型端口驱动程序， *atapi.sys*，链接到 SCSI 端口驱动程序*scsiport.sys*。

在 Microsoft Windows 2000 和 Windows XP 中，在 IDE 端口驱动程序*atapi.sys*是独立的驱动程序，不再指向*scsiport.sys*，也不会向任何其他包装器驱动程序。

为 Windows 2000 和 Windows XP 的 IDE 驱动程序模型中有三个系统提供驱动程序： *atapi.sys* （端口驱动程序）， *pciidex.sys* （控制器驱动程序） 和*pciide.sys*（泛型控制器微型驱动程序）。 下图显示了所有三个的驱动程序。

![windows 2000 和 windows xp ide 驱动程序堆栈 ](images/idedrvrs.png)

从图底部开始，下面介绍的堆栈中的每个驱动程序：

1.  Windows 2000 和 Windows XP 中的 IDE 堆栈上层 PCI 总线驱动程序。

2.  Microsoft 提供了可以管理大多数 IDE 控制器的本机 IDE 控制器驱动程序/微型驱动程序对。 IDE 控制器驱动程序， *pciidex.sys*，处理的驱动程序对和微型驱动程序，独立于硬件的方面*pciide.sys*，处理依赖于硬件的方面。

3.  供应商提供其自己 IDE 控制器微型驱动程序而不是使用本机微型驱动程序，可以选择*pciide.sys*。 供应商的微型驱动程序必须与 Microsoft 提供的控制器驱动程序，以形成一个控制器微型驱动程序对一起工作。 请参阅[Vendor-Supplied IDE 控制器微型驱动程序的要求](requirements-for-vendor-supplied-ide-controller-minidrivers.md)有关要求的说明将供应商的微型驱动程序必须满足才能正常使用本机 Microsoft 控制器驱动程序。

4.  Microsoft 提供 IDE 端口驱动程序， *atapi.sys，* 也称为*通道驱动程序*，因为它创建和管理每个 IDE 通道的功能的设备对象 (FDO)。 端口驱动程序上的 IDE 控制器/微型驱动程序对进行分层。 它将转换成所需的基础的 IDE 控制器的格式收到来自存储类驱动程序的 SCSI 请求块 (SRB)。 具体而言，为 ATAPI 和 SCSI 设备以不同的方式定义 SRB 中包含的命令描述符块 (CDB)。 端口驱动程序重新打包 Cdb 以使其与 ATAPI 传输协议，从而使失望的 IDE 总线的高级别的驱动程序兼容。

5.  Microsoft 提供了可以管理所有 CD-ROM (类型为 5 SCSI) 设备的 CD-ROM 类驱动程序。

若要查看的设备对象堆栈对应于在上图中的驱动程序堆栈关系图，请参阅[PCI IDE 控制器设备对象示例](device-object-example-for-a-pci-ide-controller.md)。

在 Windows Vista 和更高版本的操作系统，由 IDE 堆栈[ATA 端口驱动程序](ata-port-driver.md)。

 

 


