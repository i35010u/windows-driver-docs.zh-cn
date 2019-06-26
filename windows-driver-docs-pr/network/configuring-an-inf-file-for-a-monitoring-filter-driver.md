---
title: 配置监视筛选器驱动程序的 INF 文件
description: 配置监视筛选器驱动程序的 INF 文件
ms.assetid: b45c6f40-7254-4cc1-a007-d40eaa74a290
keywords:
- INF 文件 WDK 网络筛选器驱动程序
- 监视筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 968f214569d2065cd61c8b49cc24f6c2de975f21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384722"
---
# <a name="configuring-an-inf-file-for-a-monitoring-filter-driver"></a>配置监视筛选器驱动程序的 INF 文件





NDIS 筛选器驱动程序安装的以下问题是与监视筛选器驱动程序相关联：

-   设置**类**INF 文件进入**NetService** INF 文件中。 下面的示例演示一个示例**类**INF 文件项。
    ```INF
    Class = NetService
    ```

-   *DDInstall*部分中的筛选器驱动程序 INF 文件必须具有**特征**条目。 下面的示例演示如何应定义**特征**筛选器 INF 文件中的条目。

    ```INF
    Characteristics=0x40000
    ```

    而 0x40000 可值，表示 NCF\_LW\_设置筛选器 （而 0x40000 可）。 筛选器驱动程序不能设置 NCF\_筛选器 (0x400) 标志。 值 NCF\_ *Xxx*中定义标志*Netcfgx.h*。 详细了解 NCF\_ *Xxx*标记，请参阅[DDInstall 网络 INF 文件中的部分](ddinstall-section-in-a-network-inf-file.md)。

-   设置**NetCfgInstanceId**在 INF 文件中，如以下示例所示的 INF 文件条目。

    ```INF
    NetCfgInstanceId="{5cbf81bf-5055-47cd-9055-a76b2b4e3697}"
    ```

    可以使用*Uuidgen.exe*工具创建的 GUID **NetCfgInstanceId**条目。

-   *DDInstall*部分中的筛选器驱动程序的 INF 文件必须包括**Addreg**指令**Ndi**密钥。 INF 文件必须指定**服务**下的条目**Ndi**密钥。 **ServiceBinary**中的条目*服务安装*INF 文件的部分指定的筛选器驱动程序二进制文件的路径。 有关详细信息，请参阅[Adding Service-Related 值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)和[DDInstall.Services 网络 INF 文件中的部分](ddinstall-services-section-in-a-network-inf-file.md)。

-   *DDInstall*部分中的筛选器驱动程序 INF 文件必须具有**FilterType**并**FilterRunType**条目。 若要指定监视的筛选器，定义**FilterType**在 INF 文件中，如以下示例所示的条目。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000001
    ```

    **FilterType**值 0x00000001 指示筛选器是一个监视筛选器。

-   定义**FilterRunType**在 INF 文件中，如以下示例所示的条目。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000002
    ```

    在前面的示例 0x00000002 值指示筛选器模块是可选的。 若要安装必需的筛选器模块，请设置**FilterRunType** 0x00000001 的条目。 有关详细信息，请参阅[必需筛选器驱动程序](mandatory-filter-drivers.md)。

    **请注意**  我们强烈建议，监视的轻型筛选器 (LWF) 驱动程序不应为必需的除非它是用于在受控环境中，将有不可选修改 LWF 驱动程序。 这是因为必需监视 LWF 驱动程序可能会导致可选修改 LWF 驱动程序失败[ *FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)。 按照设计，以便监视所有级别的网络流量的情况下，监视的 LWF 驱动程序绑定通过每个修改的筛选器和绑定。 请考虑以下方案：
    -   通过可选的修改 LWF 驱动程序安装必需的监视 LWF 驱动程序的实例。
    -   较低的修改可选 LWF 驱动程序无法将附加到较低的组件。 这将导致在必需监视 LWF 驱动程序[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)处理程序调用。
    -   现在不加载必需的 LWF 驱动程序的实例，因为 NDIS 不会将任何协议 （如 TCP/IP) 绑定到接口或 NIC，因此呈现为不可用的接口。

     

-   下面的示例演示如何筛选器驱动程序 INF 文件指定的服务的名称。

    ```INF
    HKR, Ndi,Service,,"NdisMon"
    ```

    在此示例中，"NdisMon"是服务的驱动程序的名称，因为它将被报告到 NDIS。 请注意，筛选器驱动程序的服务的名称可以不同于驱动程序，该二进制文件的名称，但它们通常是相同。

-   下面的示例演示如何筛选器 INF 文件引用的筛选器驱动程序的服务名称时将添加该服务。
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

-   筛选器 INF 文件必须至少指定的筛选器的主服务名称**CoServices**属性，如以下示例所示。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisMon"
    ```

    有关详细信息**CoServices**属性，请参阅[Adding Service-Related 值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)。

-   **FilterClass**值 INF 文件中的筛选器驱动程序确定的修改筛选器堆栈中的顺序。 但是，监视的筛选器驱动程序未定义**FilterClass**密钥。 而是监视已安装的筛选器模块首先是最接近的微型端口适配器。

-   必须在监视的筛选器驱动程序 INF 文件，以控制驱动程序绑定中定义了以下项：

    ```INF
    HKR, Ndi\Interfaces,UpperRange,,"noupper"
    HKR, Ndi\Interfaces,LowerRange,,"nolower"
    HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
    ```

    有关控制驱动程序绑定的详细信息，请参阅[指定筛选器驱动程序绑定关系](specifying-filter-driver-binding-relationships.md)。

-   监视的筛选器 INF 文件应指定筛选器驱动程序、 与特定适配器相关联的参数和参数与特定实例 （筛选器模块） 相关联的常见参数定义。 下面的示例演示一些常见的参数定义。
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

 

 





