---
title: 注册和取消注册中断
description: 注册和取消注册中断
ms.assetid: 222782f3-092e-417d-ab1b-1988a593caa4
keywords:
- 中断 WDK 网络，注册
- 中断 WDK 网络，注销
- NdisMRegisterInterruptEx
- NdisMDeregisterInterruptEx
- 注册中断
- 注销中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3daf7e68925bfc5ade7efb6fcf4033736830ef1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842087"
---
# <a name="registering-and-deregistering-interrupts"></a>注册和取消注册中断





微型端口驱动程序调用[**NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)来注册中断。 驱动程序将[ **\_微型端口分配和初始化 NDIS，\_中断\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)结构来指定中断特征和函数入口点。 驱动程序将该结构传递给**NdisMRegisterInterruptEx**。

驱动程序调用[**NdisMDeRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)函数来释放以前通过**NdisMRegisterInterruptEx**分配的资源。

 

 





