---
title: NDKPI 的 INF 要求
description: 支持 Network Direct 内核 (NDK) 的微型端口驱动程序的 INF 文件必须满足以下要求。
ms.assetid: 1399CEB8-82A5-4F91-833E-66FC5A5663C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9af6f2d4c554b07f8f9d454b37bfeab1c0cb1e69
ms.sourcegitcommit: 791a4bb1463c8c623464a79daf0253396852fbbb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156964"
---
# <a name="inf-requirements-for-ndkpi"></a>NDKPI 的 INF 要求


支持 Network Direct 内核 (NDK) 的微型端口驱动程序的 INF 文件必须满足以下要求。

-   微型端口驱动程序的 INF 文件必须指定 Windows 组件，以发现和使用驱动程序提供服务的支持 NDK 微型端口适配器的 NDIS 范围的上界值为"ndis5"。 指定此值，如下所示：

    ```INF
    HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
    ```

-   INF 文件必须指定 **\*NetworkDirect**关键字值，如下所示。 安装该驱动程序后，管理员可以更新 **\*NetworkDirect**中的关键字值**高级**适配器属性页。 

    **请注意**中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

    ```INF
    HKR, Ndi\Params\*NetworkDirect,        ParamDesc,  0, "NetworkDirect Functionality"
    HKR, Ndi\Params\*NetworkDirect,        Type,       0, "enum"
    HKR, Ndi\Params\*NetworkDirect,        Default,    0, "1"
    HKR, Ndi\Params\*NetworkDirect\enum,   "0",        0, "Disabled"
    HKR, Ndi\Params\*NetworkDirect\enum,   "1",        0, "Enabled"
    ```

-   INF 文件必须指定 **\*NetworkDirectTechnology**关键字值，如下所示。 安装该驱动程序后，管理员可以更新 **\*NetworkDirectTechnology**中的关键字值**高级**适配器属性页。 枚举是互斥的这意味着选择某一 NetworkDirectTechnology 值排除其他所有。  这允许为平台定义严格设备行为。  
-   设备必须 express 支持的传输。  传输值是标识符映射到 WDK **NDK_RDMA_TECHNOLOGY**。  重新定义标识符被禁止。
-   具有多个并发的传输协议的设备的行为是未定义。  设备**必须**指定传输类型。

    **请注意**中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

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

    有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

    有关使用标准化的 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 
