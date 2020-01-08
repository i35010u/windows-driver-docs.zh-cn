---
title: 其他 SRB_FUNCTION_XXX 请求
description: 其他 SRB_FUNCTION_XXX 请求
ms.assetid: b0430d8e-e5cd-4f17-b77f-ec608b1469da
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_XXX 将来使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 246d8673ab9942c67a38233f4ce01d13ef36c1af
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606507"
---
# <a name="other-srb_function_xxx-requests"></a>其他 SRB_FUNCTION_XXX 请求

以下 SRB**函数**值定义为在操作系统的未来版本中使用：

- SRB_FUNCTION_RECEIVE_EVENT

- SRB_FUNCTION_RELEASE_RECOVERY

- SRB_FUNCTION_RESET_DEVICE

- SRB_FUNCTION_TERMINATE_IO

基于 NT 的操作系统 SCSI 端口驱动程序在不调用任何 SCSI 微型端口驱动程序的情况下处理具有以下 SRB**函数**值的请求：

- SRB_FUNCTION_CLAIM_DEVICE

- SRB_FUNCTION_RELEASE_QUEUE

- SRB_FUNCTION_FLUSH_QUEUE

- SRB_FUNCTION_RELEASE_DEVICE

- SRB_FUNCTION_LOCK_QUEUE

- SRB_FUNCTION_UNLOCK_QUEUE

有关这些函数的详细信息，请参阅[存储类驱动程序](introduction-to-storage-class-drivers.md)。

微型端口驱动程序设计器可以假定其微型端口驱动程序*永远不*会与上述任何一个**函数**值一起发送 SRB。 基于 NT 的操作系统端口驱动程序处理来自存储类和筛选器驱动程序的这些请求，以保护更高级别的驱动程序，使其无需访问任何特定于 HBA （或微型端口驱动程序）的状态信息来查找其设备或取消排队的请求。 这可确保基于 NT 的操作系统存储类和筛选器驱动程序不依赖于任何特定的 HBA 型号。

有关详细信息，请参阅[**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)结构。
