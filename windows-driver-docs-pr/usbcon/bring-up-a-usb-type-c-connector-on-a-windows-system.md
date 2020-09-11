---
description: '介绍 USB 连接器管理器 (UCM) ，该管理器管理 USB C # C 连接器和连接器驱动程序的预期行为。'
title: 编写 USB 类型 C 连接器驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4f6f5684489d865cb341f238e15e679165c8b8ca
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010043"
---
# <a name="write-a-usb-type-c-connector-driver"></a>编写 USB 类型 C 连接器驱动程序

需要在以下情况下编写 USB 类型 C 连接器驱动程序：

* 如果 USB Type-C 硬件能够处理 (PD) 状态机的电源交付。 否则，请考虑写入 USB 类型 C 端口控制器驱动程序。 有关详细信息，请参阅 [编写 USB 类型 C 端口控制器驱动程序](write-a-usb-type-c-port-controller-driver.md)。

* 如果你的硬件没有嵌入的控制器。 否则，加载 Microsoft 提供的内置驱动程序，UcmUcsi.sys。  (参阅用于 ACPI 传输的 [UCSI driver](ucsi.md)) 或为非 ACPI 传输 [编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md) 。

## <a name="summary"></a>摘要

* 类扩展和客户端驱动程序使用的 UCM 对象
* UCM 类扩展提供的服务
* 客户端驱动程序的预期行为

### <a name="official-specifications"></a>官方规范

* [USB 3.1 和 USB 类型-C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)
* [USB 电源交付](https://go.microsoft.com/fwlink/p/?LinkID=623310)

### <a name="applies-to"></a>适用于

* Windows 10

### <a name="wdf-version"></a>WDF 版本

* KMDF 版本1.15
* UMDF 版本2.15

## <a name="important-apis"></a>重要的 API

* [USB 类型 C 连接器驱动程序编程参考](/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

介绍 USB 连接器管理器 (UCM) ，该管理器管理 USB C # C 连接器和连接器驱动程序的预期行为。

UCM 是使用 WDF 类扩展-客户端驱动程序模型设计的。 类扩展 (UcmCx) 是 Microsoft 提供的一个 WDF 驱动程序，它提供客户端驱动程序可以调用以报告有关连接器的信息的接口。 UCM 客户端驱动程序使用连接器的硬件接口，并使类扩展能够识别连接器上出现的事件。 相反，类扩展会调用客户端驱动程序实现的回调函数以响应操作系统事件。

若要在系统上启用 USB 类型 C 连接器，必须编写客户端驱动程序。

![usb 连接器管理器](images/type-c-devnode.png)

## <a name="before-you-begin"></a>在开始之前

* 在开发计算机上 (WDK) [安装](https://go.microsoft.com/fwlink/p/?LinkID=623310)最新的 Windows 驱动程序工具包。 工具包具有编写 UCM 客户端驱动程序所需的头文件和库，具体而言，你将需要：

  * 存根库， (UcmCxstub) 。 库转换客户端驱动程序发出的调用，并将其传递给 UcmCx。
  * 标头文件 UcmCx。

    你可以编写在用户模式或内核模式下运行的 UCM 客户端驱动程序。 对于用户模式，它与 UMDF 2.x 库绑定;对于内核模式，它是 KMDF 1.15。 这两种模式的编程接口都是相同的。

    ![适用于 ucm 的 visual studio 配置](images/ucm-vs.png)

* 确定你的客户端驱动程序是否将支持 USB 类型 C 连接器的高级功能和 [Usb 电源传送](https://go.microsoft.com/fwlink/p/?LinkID=623310)。

  此支持使你能够构建包含 USB 类型 C 连接器、USB 类型 C 坞和附件以及 USB 类型 C 充电器的 Windows 设备。 客户端驱动程序报告连接器事件，这些事件允许操作系统在系统中的 USB 和电源消耗方面实现策略。

* 在目标计算机上安装适用于桌面版的 Windows 10，并使用 USB 类型 C 连接器安装 Windows 10 移动版)  (。
* 熟悉 UCM 以及它与其他 Windows 驱动程序的交互方式。 请参阅 [体系结构：适用于 Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)。
* 熟悉 Windows Driver Foundation (WDF) 。 建议读物： [开发带有 Windows Driver Foundation 的驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)（由 "Orwick" 和 "专家 Smith" 编写）。

## <a name="summary-of-the-services-provided-by-the-ucm-class-extension"></a>UCM 类扩展提供的服务摘要

UCM 类扩展使操作系统知道数据和电源角色的变化、充电级别和协商的 PD 协定。 尽管客户端驱动程序与硬件交互，但当发生这些更改时，它必须通知类扩展。 类扩展提供了一组方法，客户端驱动程序可以使用这些方法来发送)  (本主题中讨论的通知。 下面是提供的服务：

### <a name="data-role-configuration"></a>数据角色配置

在 USB 类型 C 系统上， (主机或函数) 的数据角色取决于连接器的 CC pin 状态。 你的客户端驱动程序将读取 CC 行 (参阅 [体系结构：用于 Windows 系统的 USB 类型 C 设计](architecture--usb-type-c-in-a-windows-system.md)) 端口控制器中的状态，以确定端口是否已解析为面向上游的端口 (UFP) 或下游端口 (UFP) 。 它将该信息报告给类扩展，以便它能够向 USB 角色切换驱动程序报告当前角色。

>[!NOTE]
> USB 角色切换驱动程序在 Windows 10 移动版系统上使用。 在 Windows 10 上，对于桌面版系统，类扩展和角色切换驱动程序之间的通信是可选的。 此类系统可能不使用双重角色控制器，在这种情况下，不会使用角色切换驱动程序。

### <a name="power-role-and-charging"></a>电源角色和充电

你的客户端驱动程序读取 USB 类型 C 当前广告，或与合作伙伴连接器协商一个 PD 电源协定。

* 在 Windows 10 移动版系统上，决定选择适当的充电器是软件辅助的。 客户端驱动程序将协定信息报告给类扩展，以便它可以将充电级别发送到收费仲裁驱动程序 ( # A0) 。 CAD 将选择要使用的当前级别，并将充电级别信息转发到电池子系统。
* 在适用于桌面版的 Windows 10 系统上，硬件将选择相应的充电器。 客户端驱动程序可能会选择获取此信息并将其转发给类扩展。 或者，该逻辑可能由不同的驱动程序实现。

### <a name="data-and-power-role-changes"></a>数据和电源角色更改

协商了 PD 协定后，数据角色和电源角色可能会更改。 您的客户端驱动程序或合作伙伴连接器可能会启动该更改。 客户端驱动程序将该信息报告给类扩展，以便它能够相应地重新配置内容。

### <a name="data-andor-power-role-update"></a>数据和/或电源角色更新

操作系统可能会确定当前数据角色不正确。 在这种情况下，类扩展会调用驱动程序的回调函数来执行必要的角色交换操作。

Microsoft 提供的 USB 类型-C 策略管理器监视 USB 类型 C 连接器的活动。 Windows 版本1809引入了一组编程接口，可用于将客户端驱动程序写入到策略管理器。 客户端驱动程序可参与 USB C # C 连接器的策略决策。 使用此设置，可以选择写入内核模式导出驱动程序或用户模式驱动程序。 有关详细信息，请参阅 [编写 USB 类型-C 策略管理器客户端驱动程序](policy-manager-client.md)。

## <a name="expected-behavior-of-the-client-driver"></a>客户端驱动程序的预期行为

你的客户端驱动程序负责以下任务：

* 检测对 CC 行所做的更改，并确定合作伙伴的类型，例如 UFP、DFP 等。 要执行此操作，驱动程序必须实现 USB 类型 c 规范中定义的完全类型 C 状态机。
* 根据在 "抄送" 行上检测到的方向配置 Mux。 这包括打开 PD 发送器/接收器并处理和响应 PD 消息。 要执行此操作，驱动程序必须实现 USB 电源交付2.0 规范中定义的全部 PD 接收方和发送器状态机。
* 做出 PD 策略决策，如协商 (为源或接收器) 、角色交换等。 客户端驱动程序负责确定最合适的协定。
* 播发和协商备用模式，并在检测到备用模式时配置 Mux。 客户端驱动程序负责确定要协商的备用模式。
* 通过连接器控制 VBus/VConn。

## <a name="1-initialize-the-ucm-connector-object-ucmconnector"></a>1. 初始化 UCM connector 对象 (UCMCONNECTOR) 

UCM connector 对象 (UCMCONNECTOR) 表示 USB C # C 连接器，是 UCM 类扩展和客户端驱动程序之间的主句柄。 对象跟踪连接器的运行模式和电源供电功能。

下面是客户端驱动程序检索连接器的 UCMCONNECTOR 句柄的序列的摘要。 在驱动程序的

1. 通过将引用传递给[**UCM \_ 管理器 \_ 配置**](/windows-hardware/drivers/ddi/ucmmanager/ns-ucmmanager-_ucm_manager_config)结构来调用[**UcmInitializeDevice**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucminitializedevice) 。 在调用[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之前，驱动程序必须在[**EVT_WDF_DRIVER_DEVICE_ADD**](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中调用此方法。

2. 在 [**UCM \_ 连接器 \_ TYPEC \_ CONFIG**](/windows-hardware/drivers/ddi/ucmmanager/ns-ucmmanager-_ucm_connector_typec_config) 结构中指定 USB 类型 C 连接器的初始化参数。 这包括连接器的操作模式，无论是面向下游的端口、面向上游的端口还是支持双重角色的端口。 当连接器为电源时，它还指定 USB 类型 C 当前级别。 可以设计 USB 类型 C 连接器，使其可以操作 3.5 mm 音频插孔。 如果硬件支持该功能，则必须相应地初始化连接器对象。

   在结构中，还必须注册客户端驱动程序的回调函数以处理数据角色。

   此回调函数与连接器对象相关联，该对象由 UCM 类扩展调用。 此函数必须由客户端驱动程序实现。

   [*.EVT \_ UCM \_ 连接器 \_ 设置 \_ 数据 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)  
    当连接到合作伙伴连接器时，将连接器的数据角色交换到指定的角色。

3. 如果你的客户端驱动程序想要支持 PD 功能，即处理连接器的电源交付2.0 硬件实现，则还必须初始化指定 PD 初始化参数的 [**UCM \_ 连接器 \_ PD \_ 配置**](/windows-hardware/drivers/ddi/ucmmanager/ns-ucmmanager-_ucm_connector_pd_config) 结构。 这包括电源流，无论连接器是电源接收器还是源。

   在结构中，还必须注册客户端驱动程序的回调函数以处理电源角色。

   此回调函数与连接器对象相关联，该对象由 UCM 类扩展调用。 此函数必须由客户端驱动程序实现。

   [*.EVT \_ UCM \_ 连接器 \_ 设置 \_ 电源 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)  
    将连接器的电源角色设置为在附加到合作伙伴连接器时指定的角色。

4. 调用 [**UcmConnectorCreate**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorcreate) 并检索连接器的 UCMCONNECTOR 句柄。 请确保在客户端驱动程序通过调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建框架设备对象之后调用此方法。 此调用的适当位置可以是驱动程序的 [**EVT_WDF_DEVICE_PREPARE_HARDWARE**](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 或 [**EVT_WDF_DEVICE_D0_ENTRY**](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)。

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

## <a name="2-report-the-partner-connector-attach-event"></a>2. 报告合作伙伴连接器附加事件

当检测到合作伙伴连接器的连接时，客户端驱动程序必须调用 [**UcmConnectorTypeCAttach**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecattach) 。 此调用会通知 UCM 类扩展，进而通知操作系统。 此时，系统可能会在 USB 类型 C 级别开始充电。

UCM 类扩展还通知 USB 角色切换驱动程序 (URS) 。 根据伙伴的类型，URS 将在主机角色或函数角色中配置控制器。 在调用此方法之前，请确保已正确配置系统上的 Mux。 否则，如果系统处于函数角色中，它将以不正确的速度连接 (高速而不是 SuperSpeed) 。

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

## <a name="3-report-usb-type-c-advertisement-changes"></a>3. 报告 USB 类型-C 播发更改

在初始附加事件中，伙伴连接器发送当前播发。 当 partner 为 USB 类型为 C 的下游端口时播发指定合作伙伴连接器的当前级别。 否则，播发将指定本地连接器的当前级别，由 UCMCONNECTOR 句柄 (本地连接器) 表示。 此初始播发可能会在连接的生存期内发生更改。 必须由客户端驱动程序监视这些更改。

如果本地连接器是 power 接收器，而当前播发发生了更改，则客户端驱动程序必须检测当前播发中的更改并将其报告给类扩展。 在 Windows 10 移动版系统上，CAD.sys 和电池子系统使用该信息调整其从源进行绘制的当前数量。 若要将当前级别的更改报告给类扩展，客户端驱动程序必须调用 [**UcmConnectorTypeCCurrentAdChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypeccurrentadchanged)。

## <a name="4-report-the-new-negotiated-pd-contract"></a>4. 报告新的协商 PD 约定

如果连接器支持 PD，则在初始附加事件之后，连接器及其伙伴连接器之间会传输 PD 消息。 在这两个伙伴之间，会协商一个 PD 协定，以确定连接器可以绘制的当前级别或允许合作伙伴绘制的当前级别。 每次 PD 协定发生更改时，客户端驱动程序都必须调用这些方法来报告对类扩展的更改。

* 每当客户端驱动程序获取源功能播发时，都必须调用这些方法， (来自合作伙伴的未经请求或其他) 。 仅当伙伴为源时，本地连接器 (接收器) 才能获取来自合作伙伴的未经请求的播发。 同时，本地连接器还可以从可以作为源 (的伙伴显式请求源功能，即使该伙伴当前是接收器) 也是如此。 这种交换是通过向合作伙伴发送 **获取 \_ 源 \_ cap** 消息来完成的。
  * [**UcmConnectorPdPartnerSourceCaps**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdpartnersourcecaps) 报告合作伙伴连接器公布的源功能。
  * [**UcmConnectorPdConnectionStateChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged) 报告合同的详细信息。 协定在 Power 传递2.0 规范中定义的请求数据对象中进行了介绍。
* 相反，客户端驱动程序必须在每次本地连接器 (源) 向合作伙伴公布源功能时调用这些方法。 此外，当本地连接器接收来自合作伙伴的 " **获取 \_ 源" \_ cap** 消息时，它必须使用本地连接器的源功能进行响应。
  * [**UcmConnectorPdSourceCaps**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdsourcecaps) 将系统已播发的源功能报告给伙伴连接器。
  * [**UcmConnectorPdConnectionStateChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged) 报告当前协商的 PD 协定的连接功能。

## <a name="5-report-battery-charging-status"></a>5. 报告电池充电状态

如果充电级别不充足，则客户端驱动程序可以通知 UCM 类扩展。 类扩展将此信息报告给操作系统。 系统使用该信息向用户通知显示充电器未以最佳方式向系统充电。 可以通过以下方法报告收费状态：

* [**UcmConnectorChargingStateChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorchargingstatechanged)
* [**UcmConnectorTypeCAttach**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)
* [**UcmConnectorPdConnectionStateChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)

这些方法指定充电状态。 如果报告的级别为 **UcmChargingStateSlowCharging** 或 **UcmChargingStateTrickleCharging** (参阅 [**UCM \_ 充电 \_ 状态**](/windows-hardware/drivers/ddi/ucmtypes/ne-ucmtypes-_ucm_charging_state)) ，操作系统将显示用户通知。

## <a name="6-report-pr_swapdr_swap-events"></a>6. 报告 PR \_ 交换/DR \_ 交换事件

如果连接器接收到电源角色 (PR \_ 交换) 或数据角色 (DR \_ 交换) 从伙伴交换消息，则客户端驱动程序必须通知 UCM 类扩展。

* [**UcmConnectorDataDirectionChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)

  在处理 PD DR 交换消息后调用此方法 \_ 。 在此调用后，操作系统会将新角色报告给 URS，这会泪水现有角色驱动程序并为新角色加载驱动程序。

* [**UcmConnectorPowerDirectionChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)

  处理 PD PR 交换消息后调用此方法 \_ 。 PR 交换后 \_ ，需要重新协商 PD 协定。 客户端驱动程序必须通过调用 [步骤 4](#4-report-the-new-negotiated-pd-contract)中所述的方法来报告 PD 协定协商。

## <a name="7-implement-callback-functions-to-handle-power-and-data-role-swap-requests"></a>7. 实现回调函数以处理电源和数据角色交换请求

UCM 类扩展可能会收到更改连接器的数据或电源方向的请求。 在这种情况下，它会调用客户端驱动程序的 [* \_ UCM \_ 连接器 \_ 集 \_ 数据 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role) 和 [*.evt \_ UCM \_ 连接器 \_ 集 \_ 电源 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role) 回调函数的实现， (如果连接器实现了 PD) 。 客户端驱动程序以前在其对 [**UcmConnectorCreate**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorcreate)的调用中注册了这些函数。

客户端驱动程序使用硬件接口执行角色交换操作。

* [*.EVT \_ UCM \_ 连接器 \_ 设置 \_ 数据 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)

  在回调实现中，客户端驱动程序应：

  1. 向端口伙伴发送 PD DR \_ 交换消息。
  2. 调用 [**UcmConnectorDataDirectionChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged) 以通知类扩展消息序列已成功完成或未成功完成。

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

* [*.EVT \_ UCM \_ 连接器 \_ 设置 \_ 电源 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)

    在回调实现中，客户端驱动程序应：

  1. 向端口伙伴发送一个 PD PR \_ 交换消息。
  2. 调用 [**UcmConnectorPowerDirectionChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged) 以通知类扩展消息序列已成功完成或未成功完成。

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

>[!NOTE]
>客户端驱动程序可以异步调用 [**UcmConnectorDataDirectionChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged) 和 [**UcmConnectorPowerDirectionChanged**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged) ，而不是来自回调线程。 在典型实现中，类扩展调用回调函数，这会导致客户端驱动程序启动硬件事务来发送消息。 事务完成后，硬件将通知驱动程序。 驱动程序调用这些方法来通知类扩展。

## <a name="8-report-the-partner-connector-detach-event"></a>8. 报告合作伙伴连接器分离事件

当伙伴连接器的连接结束时，客户端驱动程序必须调用 [**UcmConnectorTypeCDetach**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecdetach) 。 此调用会通知 UCM 类扩展，进而通知操作系统。

## <a name="use-case-example-mobile-device-connected-to-a-pc"></a>用例：连接到 PC 的移动设备

当运行 Windows 10 移动版的设备通过 USB 类型 C 连接连接到运行 Windows 10 版桌面版的 PC 时，操作系统将确保移动设备是面向上游端口 (UFP) ，因为 MTP 仅在该方向上起作用。 在此方案中，数据角色更正的顺序如下：

1. 在移动设备上运行的客户端驱动程序通过调用 [**UcmConnectorTypeCAttach**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecattach) 报告附加事件，并将合作伙伴连接器报告为下游的端口 (UFP) 。
2. 客户端驱动程序通过调用 [**UcmConnectorPdPartnerSourceCaps**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdpartnersourcecaps) 和 [**UCMCONNECTORPDCONNECTIONSTATECHANGED**](/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)来报告 PD 协定。
3. UCM 类扩展通知 USB 设备端驱动程序导致这些驱动程序响应来自主机的枚举。 操作系统信息通过 USB 进行交换。
4. UCM 类扩展 UcmCx 调用客户端驱动程序的回调函数来更改角色： [*.Evt \_ UCM \_ 连接器 \_ 设置 \_ 数据 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role) 和 [*.evt \_ UCM \_ 连接器 \_ 集 \_ 电源 \_ 角色*](/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)。

>[!NOTE]
>如果两个 Windows 10 移动版设备相互连接，则不会执行角色交换，并且通知用户连接不是有效的连接。

## <a name="related-topics"></a>相关主题

[为 USB 类型 C 连接器开发 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)