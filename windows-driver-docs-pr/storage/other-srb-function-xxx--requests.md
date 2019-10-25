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
ms.openlocfilehash: b41f49529b06ff831fce2f6fe0d9da4af8bc542e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842735"
---
# <a name="other-srb_function_xxx-requests"></a>其他 SRB\_函数\_XXX 请求


## <span id="ddk_other_srb_function_xxx_requests_kg"></span><span id="DDK_OTHER_SRB_FUNCTION_XXX_REQUESTS_KG"></span>


以下 SRB**函数**值定义为在操作系统的未来版本中使用：

-   SRB\_函数\_接收\_事件

-   SRB\_函数\_版本\_恢复

-   SRB\_函数\_RESET\_设备

-   SRB\_函数\_终止\_IO

基于 NT 的操作系统 SCSI 端口驱动程序在不调用任何 SCSI 微型端口驱动程序的情况下处理具有以下 SRB**函数**值的请求：

-   SRB\_函数\_声明\_设备

-   SRB\_函数\_RELEASE\_队列

-   SRB\_函数\_刷新\_队列

-   SRB\_函数\_版本\_设备

-   SRB\_函数\_锁定\_队列

-   SRB\_函数\_解锁\_队列

有关这些函数的详细信息，请参阅[存储类驱动程序](storage-class-drivers.md)。

微型端口驱动程序设计器可以假定其微型端口驱动程序*永远不*会与上述任何一个**函数**值一起发送 SRB。 基于 NT 的操作系统端口驱动程序处理来自存储类和筛选器驱动程序的这些请求，以保护更高级别的驱动程序，使其无需访问任何特定于 HBA （或微型端口驱动程序）的状态信息来查找其设备或取消排队的请求。 这可确保基于 NT 的操作系统存储类和筛选器驱动程序不依赖于任何特定的 HBA 型号。

有关详细信息，请参阅[**SCSI\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)结构。

 

 




