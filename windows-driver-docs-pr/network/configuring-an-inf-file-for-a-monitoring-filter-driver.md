---
title: 配置监视筛选器驱动程序的 INF 文件
description: 配置监视筛选器驱动程序的 INF 文件
ms.assetid: b45c6f40-7254-4cc1-a007-d40eaa74a290
keywords:
- INF 文件 WDK 网络，筛选器驱动程序
- 监视筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f38636af59c59a1239486f1c427463eb7e6b1791
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835040"
---
# <a name="configuring-an-inf-file-for-a-monitoring-filter-driver"></a>配置监视筛选器驱动程序的 INF 文件





以下 NDIS 筛选器驱动程序安装问题与监视筛选器驱动程序相关联：

-   将 INF 文件中的**类**INF 文件项设置为**空间**。 下面的示例演示了 INF 文件的示例**类**条目。
    ```INF
    Class = NetService
    ```

-   筛选器驱动程序 INF 文件中的*DDInstall*部分必须包含**特征**条目。 下面的示例演示如何在筛选 INF 文件中定义**特征**条目。

    ```INF
    Characteristics=0x40000
    ```

    0x40000 值指示已设置 NCF\_LW\_FILTER （0x40000）。 筛选器驱动程序不能设置 NCF\_FILTER （0x400）标志。 *Netcfgx*中定义了 NCF\_ *Xxx*标志的值。 有关 NCF\_ *Xxx*标志的详细信息，请参阅[网络 INF 文件中的 DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

-   在 INF 文件中设置**NetCfgInstanceId** inf 文件条目，如以下示例中所示。

    ```INF
    NetCfgInstanceId="{5cbf81bf-5055-47cd-9055-a76b2b4e3697}"
    ```

    可以使用*uuidgen.exe*工具创建**NETCFGINSTANCEID**条目的 GUID。

-   筛选器驱动程序的 INF 文件的*DDInstall*部分必须包含**Ndi**项的**Addreg**指令。 INF 文件必须在**Ndi**项下指定**服务**项。 INF 文件的 "*服务安装*" 部分中的**ServiceBinary**条目指定筛选器驱动程序的二进制文件的路径。 有关详细信息，请参阅[将与服务相关的值添加到](adding-service-related-values-to-the-ndi-key.md)[网络 INF 文件中](ddinstall-services-section-in-a-network-inf-file.md)的 Ndi Key 和 DDInstall 部分。

-   筛选器驱动程序 INF 文件中的*DDInstall*部分必须包含**FilterType**和**FilterRunType**条目。 若要指定监视筛选器，请在 INF 文件中定义**FilterType**条目，如以下示例中所示。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000001
    ```

    **FilterType**值0x00000001 表明筛选器是监视筛选器。

-   定义 INF 文件中的**FilterRunType**条目，如以下示例所示。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000002
    ```

    前面的示例中的0x00000002 值表明筛选器模块是可选的。 若要安装必需的筛选器模块，请将**FilterRunType**项设置为0x00000001。 有关详细信息，请参阅[强制筛选器驱动程序](mandatory-filter-drivers.md)。

    **请注意**  我们强烈建议您不要强制执行监视轻型筛选器（LWF）驱动程序，除非它将用于不需要修改 LWF 驱动程序的受控环境中。 这是因为必需的监视 LWF 驱动程序可能会导致可选的修改 LWF 驱动程序[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)失败。 监视 LWF 驱动程序绑定在每个修改的筛选器上，并按设计进行绑定，以便于监视所有级别的网络流量。 请考虑以下方案：
    -   必需的监视 LWF 驱动程序的实例是通过可选的修改 LWF 驱动程序安装的。
    -   修改后的可选 LWF 驱动程序无法附加到较低的组件。 这将导致不会调用必需的监视 LWF 驱动程序的[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)处理程序。
    -   由于当前未加载必需 LWF 驱动程序的实例，因此 NDIS 不会将任何协议（如 TCP/IP）绑定到接口或 NIC，从而使接口无法使用。

     

-   下面的示例演示筛选器驱动程序 INF 文件如何指定服务的名称。

    ```INF
    HKR, Ndi,Service,,"NdisMon"
    ```

    在此示例中，"NdisMon" 是驱动程序的服务的名称，因为它会报告给 NDIS。 请注意，筛选器驱动程序的服务的名称可能与驱动程序的二进制文件的名称不同，但通常是相同的。

-   下面的示例演示筛选器 INF 文件在添加该服务时如何引用筛选器驱动程序的服务的名称。
    ```INF
    [Install.Services]
    AddService=NdisMon,,NdisMon_Service_Inst

    [NdisMon_Service_Inst]
    DisplayName     = %NdisMon_Desc%
    ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
    StartType       = 1 ;SERVICE_SYSTEM_START
    ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
    ServiceBinary   = %12%\ndisMon.sys
    LoadOrderGroup  = NDIS
    Description     = %NdisMon_Desc%
    AddReg          = Common.Params.Reg
    ```

-   筛选器 INF 文件必须至少为**CoServices**属性指定筛选器的主服务名称，如下面的示例所示。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisMon"
    ```

    有关**CoServices**属性的详细信息，请参阅[将与服务相关的值添加到 Ndi 键](adding-service-related-values-to-the-ndi-key.md)。

-   筛选器驱动程序的 INF 文件中的**FilterClass**值决定了其在修改筛选器的堆栈中的顺序。 但是，监视筛选器驱动程序不会定义**FilterClass**项。 相反，首先安装的监视筛选器模块与微型端口适配器最接近。

-   你必须在监视筛选器驱动程序 INF 文件中定义以下条目来控制驱动程序绑定：

    ```INF
    HKR, Ndi\Interfaces,UpperRange,,"noupper"
    HKR, Ndi\Interfaces,LowerRange,,"nolower"
    HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
    ```

    有关控制驱动程序绑定的详细信息，请参阅[指定筛选器驱动程序绑定关系](specifying-filter-driver-binding-relationships.md)。

-   监视筛选器 INF 文件应指定筛选器驱动程序的通用参数定义、与特定适配器关联的参数，以及与特定实例关联的参数（筛选器模块）。 下面的示例演示一些常见参数定义。
    ```INF
    [Common.Params.reg]

    HKR, FilterDriverParams\DriverParam, ParamDesc, ,"Driverparam for filter"
    HKR, FilterDriverParams\DriverParam, default, ,"5"
    HKR, FilterDriverParams\DriverParam, type,  ,"int"

    HKR, FilterAdapterParams\AdapterParam, ParamDesc, ,"Adapterparam for filter"
    HKR, FilterAdapterParams\AdapterParam, default, ,"10"
    HKR, FilterAdapterParams\AdapterParam, type,  ,"int"

    HKR, FilterInstanceParams\InstanceParam, ParamDesc, ,"Instance param for filter"
    HKR, FilterInstanceParams\InstanceParam, default, ,"15"
    HKR, FilterInstanceParams\InstanceParam, type,  ,"int"
    ```

 

 





