---
title: 请勿依赖 SCSI 微型端口初始化顺序
description: 请勿依赖 SCSI 微型端口初始化顺序
ms.assetid: 762fa062-4eaa-40f2-acdb-99fc6cafe680
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- 转换 SCSI 微型端口驱动程序
- 初始化 SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储初始化
- 依赖于顺序的代码 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a16725531c16dcfc7ab93182f8b569cfe2415f52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368284"
---
# <a name="do-not-depend-on-order-of-scsi-miniport-initialization"></a>请勿依赖 SCSI 微型端口初始化顺序


## <span id="ddk_do_not_depend_on_order_of_scsi_miniport_initialization_kg"></span><span id="DDK_DO_NOT_DEPEND_ON_ORDER_OF_SCSI_MINIPORT_INITIALIZATION_KG"></span>


某些微型端口驱动程序支持在诸如 PCI、 EISA 和 ISA.等的多个不同的系统总线上的 Hba 在 Microsoft Windows NT 4.0 中，这样的微型端口驱动程序的下*HwScsiFindAdapter*微型端口驱动程序调用的顺序调用 routine(s) [ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize). 在几个情况下，这用于跟踪卡片的位置上的总线的一种类型，因此微型端口驱动程序可以避免在检测到它在另一台。

例如，假定 Twiddle PCI SCSI HBA 而言也是访问 ISA 总线上。 在 Windows NT 4.0，因为微型端口驱动程序将跟踪的调用以初始化 PCI Hba 和 ISA 总线的位置所示。 微型端口驱动程序可以使用此信息，并扫描 ISA 总线确定 I/O 范围为要跳过。

在 Windows 2000 及更高版本，此方法不再可靠。 因为插生成初始化顺序不可预测，因为微型端口驱动程序无法轻松地调用以初始化其 PCI 卡之前为其 ISA 卡扫描。 微型端口驱动程序将检测每个 PCI HBA 两次，这可能导致系统崩溃。

在这种情况下，如果 Twiddle HBA 具有可用于确定卡片的真实总线接口的命令，ISA 总线扫描无法查询找到它的每个卡。 如果卡是 PCI 卡并且不 ISA 卡，然后因为微型端口驱动程序会将其插在发出请求，以选择它之前单独。

如果微型端口驱动程序依赖于顺序的代码不能删除它必须在 Windows 2000 和更高版本的平台上运行作为旧驱动程序。

 

 




