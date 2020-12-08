---
title: IDE 端口驱动程序
description: IDE 端口驱动程序
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: f7ae5496b66e10a65415ae93557b4c3ea9504677
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835157"
---
# <a name="ide-port-driver"></a>IDE 端口驱动程序

>[!NOTE]
> ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。

在 Microsoft Windows NT 4.0 中，与 IDE 总线关联的端口/微型端口驱动程序对是一个链接到 SCSI 端口驱动程序的 SCSI 微型端口驱动程序 *atapi.sys*， *scsiport.sys*。

在 Microsoft Windows 2000 和 Windows XP 中，IDE 端口驱动程序 *atapi.sys* 是一个独立的驱动程序，它不再链接到 *scsiport.sys*，也不链接到任何其他包装驱动程序。

适用于 Windows 2000 和 Windows XP 的 IDE 驱动程序模型中提供了三个系统提供的驱动程序： *atapi.sys* (端口驱动程序) 、 *pciidex.sys* (控制器驱动程序 *) 和pciide.sys(通用* 控制器微型驱动程序) 。 下图演示了这三个驱动程序。

![windows 2000 和 windows xp ide 驱动程序堆栈 ](images/idedrvrs.png)

从图的底部开始，下面描述了堆栈中的每个驱动程序：

1. Windows 2000 和 Windows XP 中的 IDE 堆栈通过 PCI 总线驱动程序进行分层。

2. Microsoft 提供了本机 IDE 控制器驱动程序/微型驱动程序对，可管理大多数 IDE 控制器。 IDE 控制器驱动程序（ *pciidex.sys*）处理驱动程序对中独立于硬件的方面，而微型驱动程序（ *pciide.sys*）处理与硬件相关的方面。

3. 供应商可以选择提供自己的 IDE 控制器微型驱动程序，而不是使用本机微型驱动程序 *pciide.sys*。 供应商的微型驱动程序必须与 Microsoft 提供的控制器驱动程序一起使用，以形成控制器微型驱动程序对。 请参阅 [供应商提供的 IDE 控制器微型驱动程序的要求](requirements-for-vendor-supplied-ide-controller-minidrivers.md) ，以获取对供应商的微型驱动程序必须满足的要求的说明，以便在本地 Microsoft 控制器驱动程序上正常工作。

4. Microsoft 提供了一个 IDE 端口驱动程序， *atapi.sys （* 也称为 *通道驱动程序*），因为它为每个 IDE 通道创建并管理一个功能设备对象 (FDO) 。 端口驱动程序已分层为 IDE 控制器/微型驱动程序对。 它将从存储类驱动程序接收的 SCSI 请求块 (SRB) 转换为基础 IDE 控制器所需的格式。 具体而言，SRB 中包含的命令描述符块 (CDB) 的定义方式对于 ATAPI 和 SCSI 设备不同。 端口驱动程序重新打包 CDBs，使其与 ATAPI 传输协议兼容，从而将上层驱动程序与 IDE 总线的 peculiarities 分开。

5. Microsoft 提供了 CD-ROM 类驱动程序，可以管理所有 cd-rom (类型 5 SCSI) 设备。

若要查看与上图中的驱动程序堆栈相对应的设备对象堆栈的关系图，请参阅 [PCI IDE 控制器的设备对象示例](device-object-example-for-a-pci-ide-controller.md)。

在 Windows Vista 和更高版本的操作系统中，IDE 堆栈由 [ATA 端口驱动程序](ata-port-driver-overview.md)管理。
