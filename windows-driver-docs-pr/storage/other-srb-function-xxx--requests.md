---
title: 其他 SRB_FUNCTION_XXX 请求
description: 其他 SRB_FUNCTION_XXX 请求
ms.assetid: b0430d8e-e5cd-4f17-b77f-ec608b1469da
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_XXX 供将来使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecd4fbbcf8eb0b72057ca48c53f1550450723d23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389425"
---
# <a name="other-srbfunctionxxx-requests"></a>其他 SRB\_函数\_XXX 请求


## <span id="ddk_other_srb_function_xxx_requests_kg"></span><span id="DDK_OTHER_SRB_FUNCTION_XXX_REQUESTS_KG"></span>


以下 SRB**函数**值定义为在将来版本的操作系统中的使用：

-   SRB\_函数\_接收\_事件

-   SRB\_函数\_发行\_恢复

-   SRB\_函数\_重置\_设备

-   SRB\_函数\_TERMINATE\_IO

基于 NT 的操作系统 SCSI 端口驱动程序处理请求与以下 SRB**函数**值而不会调用任何 SCSI 微型端口驱动程序：

-   SRB\_函数\_声明\_设备

-   SRB\_函数\_发行\_队列

-   SRB\_函数\_刷新\_队列

-   SRB\_函数\_发行\_设备

-   SRB\_函数\_锁\_队列

-   SRB\_函数\_解锁\_队列

有关这些函数的详细信息，请参阅[存储类驱动程序](storage-class-drivers.md)。

微型端口驱动程序设计器可以假定其微型端口驱动程序将*永远不会*发送与立即上述任一 SRB**函数**值。 基于 NT 的操作系统端口驱动程序将处理这些请求存储类和筛选器驱动程序，以防止更高级别的驱动程序无需访问任何特定于 HBA 的 （或微型端口驱动程序特定） 的状态信息以查找其设备，或取消排队的请求。 这可确保基于 NT 的操作系统存储类和筛选器驱动程序 HBA 任何特定模型没有任何依赖关系。

请参阅[ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393)结构的详细信息。

 

 




