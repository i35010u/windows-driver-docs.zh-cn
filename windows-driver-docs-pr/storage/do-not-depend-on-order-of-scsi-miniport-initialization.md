---
title: 请勿依赖 SCSI 微型端口初始化顺序
description: 请勿依赖 SCSI 微型端口初始化顺序
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
- 转换 SCSI 微型端口驱动程序
- 初始化 SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储，初始化
- 与顺序相关的代码 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd7a0b2a79314db8116eb39205a4cc340051d182
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811731"
---
# <a name="do-not-depend-on-order-of-scsi-miniport-initialization"></a>请勿依赖 SCSI 微型端口初始化顺序


## <span id="ddk_do_not_depend_on_order_of_scsi_miniport_initialization_kg"></span><span id="DDK_DO_NOT_DEPEND_ON_ORDER_OF_SCSI_MINIPORT_INITIALIZATION_KG"></span>


某些微型端口驱动程序支持多个不同系统总线上的 Hba，如 PCI、EISA 和 ISA。 在 Microsoft Windows NT 4.0 下，此类微型端口驱动程序的 *HwScsiFindAdapter* 例程 (s) 按微型端口驱动程序调用 [**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)的顺序调用。 在某些情况下，这用于在一种类型的总线上跟踪卡的位置，因此微型端口驱动程序可以避免在另一种总线上检测到它。

例如，假设 Twiddle PCI SCSI HBA 还可在 ISA 总线上访问。 在 Windows NT 4.0 下，Twiddle 微型端口驱动程序将跟踪其调用了哪些 PCI Hba，并将其出现在其中。 微型端口驱动程序可以使用此信息来扫描 ISA 总线，以确定要跳过的 i/o 范围。

在 Windows 2000 和更高版本中，此方法不再可靠。 由于即插即用使初始化顺序成为不可预测的，因此可以轻松地调用 Twiddle 微型端口驱动程序，以便在初始化其 PCI 卡之前扫描其 ISA 卡。 微型端口驱动程序将检测每个 PCI HBA 两次，这可能会导致系统故障。

在这种情况下，如果 Twiddle HBA 具有可用于确定卡的实际总线接口的命令，则 ISA 总线扫描可以查询它找到的每个卡。 如果卡是 PCI 卡而不是 ISA 卡，则 Twiddle 微型端口驱动程序会将其保留，直到即插即用发出的请求选取它。

如果无法删除微型端口驱动程序的顺序相关代码，则必须在 Windows 2000 和更高版本的平台上将其作为旧驱动程序运行。

 

