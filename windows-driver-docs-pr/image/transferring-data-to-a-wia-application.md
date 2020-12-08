---
title: 将数据传输到 WIA 应用程序
description: 将数据传输到 WIA 应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b295cd5ea63d0d90111a744330a536e60d872c1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819543"
---
# <a name="transferring-data-to-a-wia-application"></a>将数据传输到 WIA 应用程序





当应用程序启动数据传输时，WIA 服务将调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法来执行传输。 此方法负责从设备获取数据，并使用 [**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) 方法将数据发送回应用程序。

在 Microsoft Windows Millennium Edition (Me) 和 Windows XP 中，WIA 微型驱动程序应该能够处理两种类型的数据传输：文件和内存。 若要确定应用程序启动的传输类型，微型驱动程序应读取 [**WIA \_ IPA \_ TYMED**](./wia-ipa-tymed.md)属性值或检查 [**MINIDRV \_ 传输 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)结构的 **TYMED** 成员。 仅当 WIA 微型驱动程序调用 [**wiasGetImageInformation**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation) 服务函数时，第二个选项才有效。 **WiasGetImageInformation** 服务函数自动读取 WIA \_ IPA \_ TYMED 属性，并将该值分配给 MINIDRV **tymed** \_ 传输上下文结构的 TYMED 成员 \_ 。

首选的方法是，WIA 微型驱动程序读取 WIA \_ IPA \_ TYMED 属性值。 这可确保微型驱动程序执行正确的购置类型。

从 Windows Vista 开始，引入了一种简化的基于流的传输方法。 有关此数据传输方法的详细信息，请参阅 [IStream 数据传输](istream-data-transfers.md)。

本部分涵盖了以下主题：

[了解 TYMED](understanding-tymed.md)

[为数据分配内存](allocating-memory-for-data.md)

[取消数据传输](canceling-a-data-transfer.md)

[取消挂起的 I/O 操作](canceling-pending-i-o-operations.md)

[原始格式数据传输](raw-format-data-transfer.md)

有关使用 TYMED ( 内存中和文件传输) 的数据传输的基本信息，请参阅 [数据传输](data-transfers.md)。

 

