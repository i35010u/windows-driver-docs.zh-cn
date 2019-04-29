---
Description: 介绍管理 USB 类型 C 连接器和连接器驱动程序的预期的行为的 USB 连接器管理器 (UCM)。
title: 编写 USB 类型 C 连接器驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 98120b794c42334977fbe6f8bbadb18f2adddf32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377475"
---
# <a name="write-a-usb-type-c-connector-driver"></a>编写 USB 类型 C 连接器驱动程序

您需要在这些情况下编写 USB 类型 C 连接器驱动程序：

-   如果您的 USB 类型 C 硬件具有处理 power 传递 (PD) 状态机的功能。 否则，请考虑编写 USB 类型 C 端口控制器驱动程序。 有关详细信息，请参阅[写入 USB 类型 C 端口控制器驱动程序](write-a-usb-type-c-port-controller-driver.md)。

-   如果您的硬件不具有嵌入式的控制器。 否则，会加载 Microsoft 提供的现成驱动程序 UcmUcsi.sys。 (请参阅[UCSI 驱动程序](ucsi.md)) 的 ACPI 传输或[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)对于非 ACPI 传输。 

**摘要**

-   UCM 对象使用的类扩展和客户端驱动程序
-   UCM 类扩展提供服务
-   客户端驱动程序的预期的行为

**正式规范**

-   [USB 3.1 和 USB 类型 C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)

**适用于：**

-   Windows 10

**WDF 版本**

-   KMDF 版本 1.15
-   UMDF 2.15 版本

**上次更新时间：**

-   2015 年 11 月

**重要的 Api**

-  [编程参考的 USB 类型 C 连接器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

介绍管理 USB 类型 C 连接器和连接器驱动程序的预期的行为的 USB 连接器管理器 (UCM)。

UCM 旨在通过使用 WDF 类扩展客户端驱动程序模型。 类扩展 (UcmCx) 是 Microsoft 提供 WDF 驱动程序，提供客户端驱动程序可以调用报告有关连接器信息的接口。 UCM 客户端驱动程序使用的连接器的硬件接口，并保留此类扩展注意连接器上发生的事件。 相反，此类扩展调用由操作系统事件的响应中的客户端驱动程序实现的回调函数。

若要启用的系统上的 USB 类型 C 连接器，必须编写客户端驱动程序。

![usb 连接器管理器](images/type-c-devnode.png)

## <a name="before-you-begin"></a>开始之前...


-   [安装](https://go.microsoft.com/fwlink/p/?LinkID=623310)最新 Windows 驱动程序工具包 (WDK) 在开发计算机上。 该工具包具有必需的标头文件和库，用于编写 UCM 客户端驱动程序，具体而言，你将需要：

    -   存根 （stub） 库中，(UcmCxstub.lib)。 库将转换所做的客户端驱动程序的调用，并将其传递到 UcmCx。
    -   标头文件，UcmCx.h。

    您可以编写一个 UCM 客户端驱动程序，在用户模式或内核模式下运行。 与 UMDF 2.x 库; 对于用户模式下，绑定适用于内核模式很 KMDF 1.15。 编程接口是相同的任何一种模式。

    ![ucm 的 visual studio 配置](images/ucm-vs.png)

-   决定您的客户端驱动程序是否支持 USB 类型 C 连接器的高级的功能和[USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)。

    此支持使您能够构建 Windows 设备使用 USB 类型 C 连接器、 USB 类型 C 停靠和附件和 USB 类型 C 充电器。 客户端驱动程序报告允许操作系统实施策略 USB 和电源消耗系统中的连接器事件。

-   Windows 10 桌面版本安装 （主页、 专业版、 企业版和教育） 在目标计算机或 Windows 10 移动版上使用 USB 类型 C 连接器。
-   熟悉 UCM 以及它如何与其他 Windows 驱动程序进行交互。 请参阅[体系结构：Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)。
-   了解使用 Windows Driver Foundation (WDF)。 推荐阅读的主题：[使用 Windows Driver Foundation 开发驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)、 由 Penny Orwick 和 Smith 专家编写。

## <a name="summary-of-the-services-provided-by-the-ucm-class-extension"></a>UCM 类扩展提供的服务的摘要


UCM 类扩展会保留在角色中数据和电源，收费级别和协商的 PD 协定的更改通知的操作系统。 虽然客户端驱动程序与硬件进行交互，它必须在这些更改发生时通知类扩展。 类扩展提供了一组客户端驱动程序可用于发送通知 （如本主题所述） 的方法。 下面是提供的服务：

-   **数据角色配置**

    在 USB C 类型系统中，数据角色 （主机或函数） 取决于抄送球瓶的连接器的状态。 客户端驱动程序读取抄送行 (请参阅[体系结构：Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)) 从端口控制器以确定该端口已解析到上游面向端口 (UFP) 或下游面向端口 (UFP) 的状态。 它报告至类扩展该信息，以便它可以向角色切换的 USB 驱动程序报告的当前角色。

    **请注意**角色切换的 USB 驱动程序使用在 Windows 10 移动版的系统上。 在桌面版本系统的 Windows 10，类扩展与角色切换驱动程序之间的通信是可选的。 此类系统可能不会使用非双角色控制器上，在这种情况下，不使用角色切换驱动程序。



-   **Power 角色和计费**

    客户端驱动程序读取 USB 类型 C 当前播发，或协商具有合作伙伴连接器的 PD power 协定。

    -   在 Windows 10 移动版系统中，选择相应的充电器的决定是软件辅助。 客户端驱动程序报告至类扩展的协定信息，以便它可以向充电仲裁驱动程序 (CAD.sys) 发送给计费级别。 CAD 选择要使用的当前级别，并将转发到电池子系统充电级别的信息。
    -   Windows 10 桌面版系统上的硬件选择适当的充电器。 客户端驱动程序可以选择获取该信息并将其转发至类扩展。 或者，可能由不同的驱动程序实现该逻辑。
-   **数据和 power 角色更改**

    已协商 PD 协定后，可能会更改数据角色和 power 角色。 所做的更改可能由客户端驱动程序或合作伙伴连接器启动。 客户端驱动程序，以便它可以重新配置相应地报告至类扩展，该信息。

-   **数据和/或 power 角色更新**

    操作系统可能会决定当前数据角色不正确。 在这种情况下则类扩展将调用您的驱动程序的回调函数来执行必要的角色交换操作。

> 提供 Microsoft USB 类型 C 策略管理器监视 USB 类型 C 连接器的活动。 Windows，版本 1809，引入了一组编程接口，可以使用它们编写到策略管理器中的客户端驱动程序。 客户端驱动程序可以参与 USB 类型 C 连接器的策略决策。 此设置后，你可以选择要写入的内核模式导出驱动程序或用户模式驱动程序。 有关详细信息，请参阅[写入 USB 类型 C 策略管理器客户端驱动程序](policy-manager-client.md)。

## <a name="expected-behavior-of-the-client-driver"></a>客户端驱动程序的预期的行为


客户端驱动程序是负责执行这些任务：

-   检测抄送行上的更改，并确定的合作伙伴，如 UFP、 DFP，以及其他类型。 若要执行此操作，该驱动程序必须实现完整类型 C 状态机 USB 类型 C 规范中定义。
-   配置你 Mux 基于抄送行上检测到的方向。 这包括开启 PD 传输器/接收器和处理以及响应 PD 消息。 若要执行此操作，该驱动程序必须实现的完整 PD 接收器和发射器状态机 USB Power 交付 2.0 规范中定义。
-   请 PD 策略决策，例如协商 （作为源或接收器） 的协定、 角色交换和其他人。 客户端驱动程序负责确定最合适的协定。
-   播发和协商其他模式，并配置 Mux，如果检测到的备用模式。 客户端驱动程序负责决定要协商的备用模式。
-   对连接器的 VBus/VConn 控制。

## <a name="1-initialize-the-ucm-connector-object-ucmconnector"></a>1.初始化 UCM 连接器对象 (UCMCONNECTOR)


UCM 连接器对象 (UCMCONNECTOR) 表示 USB 类型 C 连接器，并且是 UCM 类扩展和客户端驱动程序之间的主要句柄。 对象跟踪该连接器的运行模式以及 power 溯源功能。

下面是序列的客户端驱动程序在其中检索连接器的 UCMCONNECTOR 句柄的摘要。 在您的驱动程序中执行这些任务

1.  调用[ **UcmInitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/mt187920)由传递到引用[ **UCM\_MANAGER\_配置**](https://msdn.microsoft.com/library/windows/hardware/mt187932)结构。 该驱动程序必须调用此方法[ **EVT_WDF_DRIVER_DEVICE_ADD** ](https://msdn.microsoft.com/library/windows/hardware/ff541693)之前调用的回调函数[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。

2.  初始化为指定参数中的 USB 类型 C connector [ **UCM\_连接器\_TYPEC\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/mt187930)结构。 这包括运行模式的连接器，它是面向下游的端口，面向上游的端口，或者是双角色是否支持。 在电源连接器时，它还指定 USB 类型 C 当前级别。 可以设计 USB 类型 C 连接器，以便其行为与 3.5mm 音频插孔。 如果硬件支持的功能，必须相应地初始化连接器对象。

    在结构中，还必须注册用于处理数据角色的客户端驱动程序的回调函数。

    此回调函数是与连接器对象，该调用 UCM 类扩展的对象相关联。 此函数必须由客户端驱动程序实现。

    [*EVT\_UCM\_CONNECTOR\_SET\_DATA\_ROLE*](https://msdn.microsoft.com/library/windows/hardware/mt187818)  
    交换到指定角色时附加到合作伙伴连接器的连接器的数据角色。

3.  如果客户端驱动程序的目标是支持 PD 的即处理的连接器的 Power 交付 2.0 硬件实现，还必须初始化[ **UCM\_连接器\_PD\_配置**](https://msdn.microsoft.com/library/windows/hardware/mt187924)结构，它指定 PD 初始化参数。 这包括电源、 流连接器是否 power 接收器或源。

    在结构中，还必须注册用于处理 power 角色的客户端驱动程序的回调函数。

    此回调函数是与连接器对象，该调用 UCM 类扩展的对象相关联。 此函数必须由客户端驱动程序实现。

    [*EVT\_UCM\_CONNECTOR\_SET\_POWER\_ROLE*](https://msdn.microsoft.com/library/windows/hardware/mt187819)  
    将连接器的 power 角色设置为指定的角色附加到合作伙伴连接器时。

4.  调用[ **UcmConnectorCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt187909)和检索连接器的 UCMCONNECTOR 句柄。 请确保客户端驱动程序已通过调用创建 framework 设备对象后调用此方法[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。 此调用的合适位置可以是驱动程序的[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://msdn.microsoft.com/library/windows/hardware/ff540880)或[ **EVT_WDF_DEVICE_D0_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff540848)。

```cpp
EVT_UCM_CONNECTOR_SET_DATA_ROLE     EvtSetDataRole;

NTSTATUS
EvtDevicePrepareHardware(
    WDFDEVICE Device,
    WDFCMRESLIST ResourcesRaw,
    WDFCMRESLIST ResourcesTranslated
    )
{
    NTSTATUS status = STATUS_SUCCESS;
    PDEVICE_CONTEXT devCtx;
    UCM_MANAGER_CONFIG ucmCfg;
    UCM_CONNECTOR_CONFIG connCfg;
    UCM_CONNECTOR_TYPEC_CONFIG typeCConfig;
    UCM_CONNECTOR_PD_CONFIG pdConfig;
    WDF_OBJECT_ATTRIBUTES attr;
    PCONNECTOR_CONTEXT connCtx;

    UNREFERENCED_PARAMETER(ResourcesRaw);
    UNREFERENCED_PARAMETER(ResourcesTranslated);

    TRACE_FUNC_ENTRY();

    devCtx = GetDeviceContext(Device);

    if (devCtx->Connector)
    {
        goto Exit;
    }

    //
    // Initialize UCM Manager
    //
    UCM_MANAGER_CONFIG_INIT(&ucmCfg);

    status = UcmInitializeDevice(Device, &ucmCfg);
    if (!NT_SUCCESS(status))
    {
        TRACE_ERROR(
            "UcmInitializeDevice failed with %!STATUS!.",
            status);
        goto Exit;
    }

    TRACE_INFO("UcmInitializeDevice() succeeded.");

    //
    // Create a USB Type-C connector #0 with PD
    //
    UCM_CONNECTOR_CONFIG_INIT(&connCfg, 0);

    UCM_CONNECTOR_TYPEC_CONFIG_INIT(
        &typeCConfig,
        UcmTypeCOperatingModeDrp,
        UcmTypeCCurrentDefaultUsb | UcmTypeCCurrent1500mA | UcmTypeCCurrent3000mA);

    typeCConfig.EvtSetDataRole = EvtSetDataRole;

    UCM_CONNECTOR_PD_CONFIG_INIT(&pdConfig, UcmPowerRoleSink | UcmPowerRoleSource);

    connCfg.TypeCConfig = &typeCConfig;
    connCfg.PdConfig = &pdConfig;

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attr, CONNECTOR_CONTEXT);

    status = UcmConnectorCreate(Device, &connCfg, &attr, &devCtx->Connector);
    if (!NT_SUCCESS(status))
    {
        TRACE_ERROR(
            "UcmConnectorCreate failed with %!STATUS!.",
            status);
        goto Exit;
    }

    connCtx = GetConnectorContext(devCtx->Connector);

    UcmEventInitialize(&connCtx->EventSetDataRole);

    TRACE_INFO("UcmConnectorCreate() succeeded.");

Exit:

    TRACE_FUNC_EXIT();
    return status;
}
```

## <a name="2-report-the-partner-connector-attach-event"></a>2.合作伙伴连接器将附加事件的报表


客户端驱动程序必须调用[ **UcmConnectorTypeCAttach** ](https://msdn.microsoft.com/library/windows/hardware/mt187915)时检测到合作伙伴连接器的连接。 此调用通知 UCM 类扩展，从而进一步通知操作系统。 此时系统可能会开始计费 USB 类型 C 级别。

UCM 类扩展也会通知 USB 角色切换驱动程序 (URS)。 URS 根据伙伴的类型，配置主机角色或函数角色中的控制器。 调用此方法之前，请确保你的系统上 Mux 已正确配置。 否则，如果系统处于函数角色，它将以不正确的速度 （而不是 SuperSpeed 高速） 连接。

```cpp
        UCM_CONNECTOR_TYPEC_ATTACH_PARAMS attachParams;

        UCM_CONNECTOR_TYPEC_ATTACH_PARAMS_INIT(
            &attachParams,
            UcmTypeCPortStateDfp);
        attachParams.CurrentAdvertisement = UcmTypeCCurrent1500mA;

        status = UcmConnectorTypeCAttach(
                    Connector,
                    &attachParams);
        if (!NT_SUCCESS(status))
        {
            TRACE_ERROR(
                "UcmConnectorTypeCAttach() failed with %!STATUS!.",
                status);
            goto Exit;
        }

        TRACE_INFO("UcmConnectorTypeCAttach() succeeded.");
```

## <a name="3-report-usb-type-c-advertisement-changes"></a>3.报表 USB 类型 C 播发更改


在初始的附加事件，合作伙伴连接器发送的当前播发。 如果当合作伙伴是 USB 类型-C 面向下游的端口时，播发指定合作伙伴连接器的当前级别。 否则，播发指定本地连接器，由 UCMCONNECTOR 句柄 （本地连接器） 表示的当前级别。 在连接的生存期期间可能会更改此初始播发。 这些更改必须受客户端驱动程序。

如果本地连接器的 power 接收器和当前播发更改，客户端驱动程序必须检测当前播发中的更改，并报告这些至类扩展。 在 Windows 10 移动版系统中，该信息用于通过 CAD.sys 和电池子系统调整的当前源中绘制的量。 若要向此类扩展报告当前级别中的更改，客户端驱动程序必须调用[ **UcmConnectorTypeCCurrentAdChanged**](https://msdn.microsoft.com/library/windows/hardware/mt187916)。

## <a name="4-report-the-new-negotiated-pd-contract"></a>4.报告新协商 PD 协定


如果连接器支持 PD，初始附加事件后，有 PD 连接器和其合作伙伴连接器之间传输的消息。 这两个合作伙伴之间进行协商 PD 协定，用于确定当前级别连接器可以绘制或允许该合作伙伴要绘制。 每次 PD 协定更改，客户端驱动程序必须调用这些方法来报告更改至类扩展。

-   客户端驱动程序必须调用这些方法，每当它从合作伙伴获取源功能播发 （未经请求或其他方式）。 仅当合作伙伴为源时，本地连接器 （接收器） 从合作伙伴获取未经请求的播发。 此外，本地连接器可以显式请求源功能从合作伙伴能够成为源 （即使合作伙伴当前是接收器）。 交换可通过发送**获取\_源\_Caps**到合作伙伴的消息。
    -   [**UcmConnectorPdPartnerSourceCaps** ](https://msdn.microsoft.com/library/windows/hardware/mt187912)报告所播发的合作伙伴连接器的源功能。
    -   [**UcmConnectorPdConnectionStateChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187911)报告约定的详细信息。 中电源交付 2.0 规范中定义的请求数据对象描述协定。
-   相反，客户端驱动程序必须调用这些方法每次本地连接器 （源） 播发到合作伙伴的源功能。 此外，当在本地连接器收到**获取\_源\_Caps**消息从合作伙伴，它必须响应与本地连接器的源功能。
    -   [**UcmConnectorPdSourceCaps** ](https://msdn.microsoft.com/library/windows/hardware/mt187913)报告已播发到合作伙伴连接器系统的源功能。
    -   [**UcmConnectorPdConnectionStateChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187911)报表连接功能的当前协商 PD 协定。

## <a name="5-report-battery-charging-status"></a>5.报表电池充电状态


客户端驱动程序可以通知 UCM 类扩展，如果充电级别是不够的。 类扩展报告操作系统到此信息。 系统使用该信息来显示用户通知的充电器未以最佳方式在充电系统。 可以通过这些方法报告充电状态：

-   [**UcmConnectorChargingStateChanged**](https://msdn.microsoft.com/library/windows/hardware/mt187908)
-   [**UcmConnectorTypeCAttach**](https://msdn.microsoft.com/library/windows/hardware/mt187915)
-   [**UcmConnectorPdConnectionStateChanged**](https://msdn.microsoft.com/library/windows/hardware/mt187911)

这些方法指定充电状态。 如果报告的级别，则**UcmChargingStateSlowCharging**或**UcmChargingStateTrickleCharging** (请参阅[ **UCM\_正在充电\_状态** ](https://msdn.microsoft.com/library/windows/hardware/mt187921))，操作系统显示用户通知。

## <a name="6-report-prswapdrswap-events"></a>6.报告 PR\_交换/DR\_交换事件


如果连接器会收到 power 角色 (PR\_交换) 或数据角色 (灾难恢复\_交换) 的客户端驱动程序必须通知 UCM 类扩展从合作伙伴交换消息。

-   [**UcmConnectorDataDirectionChanged**](https://msdn.microsoft.com/library/windows/hardware/mt187910)

    调用此方法后 PD DR\_处理交换消息。 此调用后，操作系统向 URS 消除现有角色驱动程序并加载驱动程序，为新角色报告的新角色。

-   [**UcmConnectorPowerDirectionChanged**](https://msdn.microsoft.com/library/windows/hardware/mt187914)

    PD 拉取请求后，调用此方法\_处理交换消息。 PR 后\_交换，需要重新协商 PD 协定。 客户端驱动程序必须通过调用中所述的方法来报告该 PD 合同谈判[步骤 4](#pd-contract)。

## <a name="7-implement-callback-functions-to-handle-power-and-data-role-swap-requests"></a>7.实现回调函数来处理能力和数据角色交换请求


UCM 类扩展可能会收到请求更改的连接器的数据或电源方向。 在这种情况下，它调用的客户端驱动程序实现[ *EVT\_UCM\_连接器\_设置\_数据\_角色*](https://msdn.microsoft.com/library/windows/hardware/mt187818)和[*EVT\_UCM\_连接器\_设置\_POWER\_角色*](https://msdn.microsoft.com/library/windows/hardware/mt187819)回调函数 （如果连接器实现 PD）。 客户端驱动程序之前对其调用中注册这些函数[ **UcmConnectorCreate**](https://msdn.microsoft.com/library/windows/hardware/mt187909)。

客户端驱动程序只需使用硬件接口，这样就可以执行角色交换操作。

-   [*EVT\_UCM\_CONNECTOR\_SET\_DATA\_ROLE*](https://msdn.microsoft.com/library/windows/hardware/mt187818)

    在回调实现中，客户端驱动程序应为：

    1.  发送 PD DR\_到端口合作伙伴交换消息。
    2.  调用[ **UcmConnectorDataDirectionChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187910)通知成功或未成功完成的消息序列的类扩展。

    ```cpp
    EVT_UCM_CONNECTOR_SET_DATA_ROLE     EvtSetDataRole;  

    NTSTATUS  
    EvtSetDataRole(  
        UCMCONNECTOR  Connector,  
        UCM_TYPE_C_PORT_STATE DataRole  
        )  
    {  
        PCONNECTOR_CONTEXT connCtx;  

        TRACE_INFO("EvtSetDataRole(%!UCM_TYPE_C_PORT_STATE!) Entry", DataRole);  

        connCtx = GetConnectorContext(Connector);

        TRACE_FUNC_EXIT();  

        return STATUS_SUCCESS;  
    }  
    ```


-   [*EVT\_UCM\_CONNECTOR\_SET\_POWER\_ROLE*](https://msdn.microsoft.com/library/windows/hardware/mt187819)

    在回调实现中，客户端驱动程序应为：

    1.  发送 PD PR\_到端口合作伙伴交换消息。
    2.  调用[ **UcmConnectorPowerDirectionChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187914)通知成功或未成功完成的消息序列的类扩展。

    ```cpp
    EVT_UCM_CONNECTOR_SET_POWER_ROLE     EvtSetPowerRole;  

    NTSTATUS  
    EvtSetPowerRole(  
        UCMCONNECTOR Connector,  
        UCM_POWER_ROLE PowerRole  
        )  
    {  
        PCONNECTOR_CONTEXT connCtx;  

        TRACE_INFO("EvtSetPowerRole(%!UCM_POWER_ROLE!) Entry", PowerRole);  

        connCtx = GetConnectorContext(Connector);  

        //PR_Swap operation.  
        
        TRACE_FUNC_EXIT();  

        return STATUS_SUCCESS;  
    }  
    ```


**注意**  
客户端驱动程序可以调用[ **UcmConnectorDataDirectionChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187910)并[ **UcmConnectorPowerDirectionChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187914)以异步方式这不是从回调线程。 在典型的实现中，此类扩展调用导致客户端驱动程序，以启动硬件事务将消息发送的回调函数。 当事务完成后时，硬件会通知驱动程序。 该驱动程序调用这些方法，以通知此类扩展。



## <a name="8-report-the-partner-connector-detach-event"></a>8.合作伙伴连接器分离事件报表


客户端驱动程序必须调用[ **UcmConnectorTypeCDetach** ](https://msdn.microsoft.com/library/windows/hardware/mt187918)与合作伙伴连接器连接结束时。 此调用通知 UCM 类扩展，从而进一步通知操作系统。

## <a name="use-case-example-mobile-device-connected-to-a-pc"></a>使用情况示例：连接到电脑的移动设备


当运行 Windows 10 移动版的设备连接到通过 USB 类型 C 连接的桌面版本中运行 Windows 10 的 PC 时，操作系统可确保该移动设备是上游面向端口 (UFP)，因为 MTP 将仅在该方向中正常运行。 在此方案中，下面是用于数据角色更正序列：

1.  在移动设备上运行的客户端驱动程序通过调用报告的附加事件[ **UcmConnectorTypeCAttach** ](https://msdn.microsoft.com/library/windows/hardware/mt187915)并报告合作伙伴连接器为下游面向端口 (UFP)。
2.  客户端驱动程序通过调用报告 PD 协定[ **UcmConnectorPdPartnerSourceCaps** ](https://msdn.microsoft.com/library/windows/hardware/mt187912)并[ **UcmConnectorPdConnectionStateChanged** ](https://msdn.microsoft.com/library/windows/hardware/mt187911).
3.  UCM 类扩展会导致这些驱动程序以响应来自主机的枚举的 USB 设备端驱动程序通知。 通过 USB 交换操作系统信息。
4.  UCM 类扩展 UcmCx 调用客户端驱动程序的回调函数来更改角色：[*EVT\_UCM\_连接器\_设置\_数据\_角色*](https://msdn.microsoft.com/library/windows/hardware/mt187818)并[ *EVT\_UCM\_连接器\_设置\_电源\_角色*](https://msdn.microsoft.com/library/windows/hardware/mt187819)。

**请注意**如果两个 Windows 10 移动版设备连接到每个其他、 不执行角色交换，并通知用户该连接不是有效的连接。



## <a name="related-topics"></a>相关主题
[为 USB 类型 C 连接器开发 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)  



