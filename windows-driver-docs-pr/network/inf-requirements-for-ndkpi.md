---
title: NDKPI 的 INF 要求
description: 支持网络直接内核 (NDK) 的微型端口驱动程序的 INF 文件必须满足以下要求。
ms.assetid: 1399CEB8-82A5-4F91-833E-66FC5A5663C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc96cbde91cf0b206445a16367948f1efdc557b4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212389"
---
# <a name="inf-requirements-for-ndkpi"></a>NDKPI 的 INF 要求


支持网络直接内核 (NDK) 的微型端口驱动程序的 INF 文件必须满足以下要求。

-   小型端口驱动程序的 INF 文件必须指定一个 NDIS 上限范围值 "ndis5"，才能让 Windows 组件发现和使用由驱动程序提供服务的支持 NDK 的微型端口适配器。 此值的指定方式如下：

    ```INF
    HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
    ```

-   INF 文件必须按如下所示指定** \* NetworkDirect**关键字值。 安装驱动程序后，管理员可以在适配器的 "**高级**" 属性页中更新 " ** \* NetworkDirect**关键字" 值。 

    **注意**   在适配器的 " **高级** " 属性页中进行更改后，会自动重新启动微型端口驱动程序。

    ```INF
    HKR, Ndi\Params\*NetworkDirect,        ParamDesc,  0, "NetworkDirect Functionality"
    HKR, Ndi\Params\*NetworkDirect,        Type,       0, "enum"
    HKR, Ndi\Params\*NetworkDirect,        Default,    0, "1"
    HKR, Ndi\Params\*NetworkDirect\enum,   "0",        0, "Disabled"
    HKR, Ndi\Params\*NetworkDirect\enum,   "1",        0, "Enabled"
    ```

-   INF 文件必须按如下所示指定** \* NetworkDirectTechnology**关键字值。 安装驱动程序后，管理员可以在适配器的 "**高级**" 属性页中更新** \* NetworkDirectTechnology**关键字值。 枚举是互斥的，也就是说，NetworkDirectTechnology 值的选择不包括所有其他值。  这允许平台定义严格的设备行为。  
-   设备必须仅表示支持的传输。  传输值是映射到 WDK **NDK_RDMA_TECHNOLOGY**的标识符。  禁止重定义标识符。
-   具有多个并发传输的设备的行为是不确定的。  设备 **必须** 指定传输类型。

    **注意**   在适配器的 " **高级** " 属性页中进行更改后，会自动重新启动微型端口驱动程序。

    ```INF
    HKR, Ndi\Params\*NetworkDirectTechnology,        ParamDesc,  0,  "NetworkDirect Technology"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Default,    0,  "1"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Type,       0,  "enum"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   1,          0,  "iWARP"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   2,          0,  "InfiniBand"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   3,          0,  "RoCE"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   4,          0,  "RoCEv2"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Optional,   0,  "0"
    ```

    有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

    有关使用标准 INF 关键字的详细信息，请参阅 [网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

