---
title: 设置本地的 NDIS QoS 参数
description: 设置本地的 NDIS QoS 参数
ms.assetid: 7AB30829-16A0-46BF-8066-506E01E718A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8e499fbe42c94322009b239b82400cb4988fd60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534516"
---
# <a name="setting-local-ndis-qos-parameters"></a>设置本地的 NDIS QoS 参数


本地 NDIS 服务质量 (QoS) 参数指定的微型端口驱动程序和其网络适配器的预配本地 QoS 设置。 微型端口驱动程序中通过以下方式获取本地的 NDIS QoS 参数：

-   通过的对象标识符 (OID) 方法请求[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)数据中心桥接 (DCB) 组件 (Msdcb.sys) 颁发。 此 OID 请求包含[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，它指定本地的 NDIS QoS 参数。

    有关 DCB 组件的详细信息，请参阅[NDIS QoS 体系结构的数据中心桥接](ndis-qos-architecture-for-data-center-bridging.md)。

    **请注意**  从 Windows Server 2012 开始，DCB 组件安装并启用与 Microsoft 数据中心桥接 (DCB) 服务器功能。 默认情况下未安装此功能。

     

-   通过在系统注册表中存储和网络适配器的独立硬件供应商 (IHV) 所定义的专有设置。 微型端口驱动程序将读取这些设置时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) NDIS 调用函数。

-   通过颁发给微型端口驱动程序通过由 IHV 开发管理应用程序特有的设置。

DCB 组件时发出的 OID 方法请求[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)，则**NDIS\_QOS\_参数\_WILLING**的标志**NDIS\_QOS\_参数。标志**成员指定微型端口驱动程序如何解析从本地的 NDIS QoS 参数及其操作 QoS 参数。 根据此标志，驱动程序将按以下方式解决本地 QoS 参数：

-   如果**NDIS\_QOS\_参数\_WILLING**设置标志，微型端口驱动程序必须启用本地 DCB 交换 (DCBX) 愿意状态。 这将允许驱动程序进行远程配置与 QoS 参数。 在这种情况下，该驱动程序解析其操作的 QoS 参数基于远程 QoS 参数。

    微型端口驱动程序也可以解决基于由 IHV 定义任何专有 QoS 设置其操作的 QoS 参数。 该驱动程序可以仅执行此操作未配置远程对等方或本地操作系统的 QoS 参数。

    有关此过程的详细信息，请参阅[接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

-   如果**NDIS\_QOS\_参数\_WILLING**未设置标志，微型端口驱动程序必须禁用本地 DCBX 愿意状态。 这将允许驱动程序解析其操作的 QoS 参数从其本地 QoS 参数而不是远程的 QoS 参数。

    **请注意**  微型端口驱动程序如果禁用了本地 DCBX 愿意状态，仍可以接受远程 QoS 参数，但不能使用它们解析其操作的 QoS 参数。

     

如果禁用了本地 DCBX 愿意状态，则微型端口驱动程序管理其本地 QoS 参数时必须遵循以下准则：

-   微型端口驱动程序，需要禁用或为其重写任何本地 QoS 参数的相关**NDIS\_QOS\_参数\_*Xxx*\_配置**未设置标志**NDIS\_QOS\_参数。标志**成员。

    例如，微型端口驱动程序可以重写由 IHV 定义其专有设置 QoS 参数是未配置本地 QoS 参数。 如果未使用指定的本地 QoS 参数没有专有设置**NDIS\_QOS\_参数\_*Xxx*\_配置**标志，该驱动程序必须禁用这些网络适配器上的 QoS 参数。

    **请注意**  NDIS 可保证这两种**NDIS\_QOS\_参数\_ETS\_配置**并**NDIS\_QOS\_参数\_PFC\_配置**标志是设置或清除在一起。

     

-   微型端口驱动程序应*应用*中包含的本地 QoS 参数[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构时它解析其操作的 NDIS QoS 参数。 如果要将驱动程序应用这些本地 QoS 参数，它必须使用它来自远程对等方的任何远程 QoS 参数。

    此过程的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

有关本地 DCBX 愿意状态，请参阅[管理本地 DCBX 愿意状态](managing-the-local-dcbx-willing-state.md)。

 

 





