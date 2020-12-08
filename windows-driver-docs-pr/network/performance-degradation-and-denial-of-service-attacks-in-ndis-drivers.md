---
title: NDIS 驱动程序中的性能降低和 DoS 攻击
description: NDIS 驱动程序中的性能下降和拒绝服务攻击
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb85bb74151655b95cd98beec214a59f579f071
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822866"
---
# <a name="performance-degradation-and-denial-of-service-attacks-in-ndis-drivers"></a>NDIS 驱动程序中的性能下降和拒绝服务攻击




如果 NDIS 驱动程序中断处理程序分析收到的数据包，中断处理程序实现可能会导致性能下降和拒绝服务攻击。 例如，恶意用户可以通过发送多个数据包来面向计算机，使微型端口驱动程序忙于计算中断处理程序中错误数据包上的校验和。

即使您对驱动程序处理收到的数据包有一定的了解，驱动程序也会在派单 IRQL 执行接收操作。 相反，应让驱动程序堆栈处理接收的数据包。 在这种情况下，过量驱动程序堆栈可能会复制数据包，并在以后对其进行操作。

 

 





