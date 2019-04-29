---
title: 性能下降，NDIS 驱动程序中的 DoS 攻击
description: NDIS 驱动程序中的性能下降和拒绝服务攻击
ms.assetid: 0e80c6e2-3e6d-4189-b2df-bdd9a4a40dd6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ee2aa40e48fb33f4e27e8c687389dd5598242be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366734"
---
# <a name="performance-degradation-and-denial-of-service-attacks-in-ndis-drivers"></a>NDIS 驱动程序中的性能下降和拒绝服务攻击




如果 NDIS 驱动程序中断处理程序将分析接收到的数据包，中断处理程序实现可能会导致性能下降，拒绝服务攻击。 例如，恶意用户可以发送多个数据包，以便微型端口驱动程序正忙计算中断处理程序中的错误数据包上的校验和目标计算机。

即使你非常小心在您的驱动程序如何处理接收到的数据包，该驱动程序将执行接收操作在调度 IRQL。 相反，应让驱动程序堆栈处理接收到的数据包。 在这种情况下，基础驱动程序堆栈可能复制数据包并对其进行更高版本在被动 irql 下完成。

 

 





