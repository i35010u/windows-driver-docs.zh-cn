---
title: NDIS 接口信息
description: NDIS 接口信息
ms.assetid: 35187fda-a239-4801-b0be-53fcbee7d24e
keywords:
- 管理信息基本 WDK 网络
- Mib WDK 网络
- NDIS WDK 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156aaedf81de9b0b0b7cb14538ad0cc5dd7e252b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542892"
---
# <a name="ndis-interface-information"></a>NDIS 接口信息





标准化的接口，用于查询 NDIS 管理信息库 (Mib) 简化的过量驱动程序和用户模式应用程序有关的网络接口的查询信息。 MIB 客户端调用请求信息从基础的 NDIS 接口提供程序的 NDIS 提供的函数。 这将导致 NDIS 发出 OID 请求来检索该信息。 若要提供给客户端的信息，NDIS 调用客户端注册到 NDIS 的回调函数。

有关 NDIS 网络接口服务的详细信息，请参阅[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566525)。

NDIS 提供增强的支持为 Management Instrumentation (WMI)。 有关 WMI 的 NDIS 6.0 支持的详细信息，请参阅[NDIS 支持 WMI](ndis-support-for-wmi.md)。

## <a name="related-topics"></a>相关主题


[**NDIS\_接口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565736)

 

 






