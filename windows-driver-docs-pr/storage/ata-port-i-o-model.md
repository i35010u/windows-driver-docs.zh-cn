---
title: ATA 端口 I/O 模型
description: ATA 端口 I/O 模型
ms.assetid: 6feaf2c4-63b2-4ab2-9d4d-7259406be652
keywords:
- ATA 端口驱动程序 WDK I/O
- I/O WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 402b4a219759dd92d834ce0fdb2debab27dc9e7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368399"
---
# <a name="ata-port-io-model"></a>ATA 端口 I/O 模型


## <span id="ddk_ata_port_i_o_model_kg"></span><span id="DDK_ATA_PORT_I_O_MODEL_KG"></span>

**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。



ATA 端口驱动程序，就像 Storport 驱动程序，使用 I/O 的推送模型。 这意味着该驱动程序将以异步方式对其微型端口驱动程序，最大数量的重叠数据包的 I/O 请求转发而无需等待微型端口驱动程序请求的输入。 在推送模型中，端口驱动程序控制的 I/O 请求流，并将推送到微型端口驱动程序的请求。

另一方面，SCSI 端口驱动程序使用 I/O 请求的模型。 在请求模型中的 I/O，SCSI 端口驱动程序以同步方式将转发到其微型端口驱动程序的 I/O 请求并等待微型端口驱动程序，以请求新的输入，再发送下一步的 I/O 请求。 此外，微型端口驱动程序控制的 I/O 请求流和端口驱动程序中向下拉取请求。

Storport 驱动程序的 I/O 模型的详细信息，请参阅[Storport I/O 模型](storport-i-o-model.md)。

SCSI 端口驱动程序的 I/O 模型的详细信息，请参阅[SCSI 端口 I/O 模型](scsi-port-i-o-model.md)。

 

 


