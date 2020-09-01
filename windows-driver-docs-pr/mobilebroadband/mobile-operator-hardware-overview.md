---
title: 移动运营商硬件概述
description: 移动运营商硬件概述
ms.assetid: b2322972-16be-443f-b46a-7834b4d7ead0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b25ebb1c3dd57dc3013070ff3d82e076be65126
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212213"
---
# <a name="mobile-operator-hardware-overview"></a>移动运营商硬件概述


你应使用本主题来深入了解 Windows 8、Windows 8.1 以及 Windows 10 移动宽带硬件要求和建议。 建议使用以下方式为客户提供简化的连接体验，并减少维护和支持成本。

-   提供 USB 接口的嵌入式移动宽带模块必须符合 Windows 8、Windows 8.1 或 Windows 10 硬件认证要求，并使用移动宽带类驱动程序进行管理。 适用于 Ihv 的硬件要求文档应要求移动宽带设备通过 Windows 8、Windows 8.1 或 Windows 10 设备认证。

-   外部 USB 移动宽带连接器必须支持标识变形。 适用于 Ihv 的硬件要求文档应要求外部移动宽带设备同时通过 Windows 8 设备认证、Windows 8.1 或 Windows 10 设备认证，并通过 Windows 7 徽标认证。

    -   在 Windows 10 计算机上，转换器显示为 Windows 10 认证的移动宽带设备，并使用移动宽带类驱动程序进行管理。

    -   在 Windows 8.1 计算机上，转换器显示为 Windows 8.1 认证的移动宽带设备，并使用移动宽带类驱动程序进行管理。

    -   在 Windows 8 计算机上，转换器显示为 Windows 8 认证的移动宽带设备，并使用移动宽带类驱动程序进行管理。

    -   在 Windows 7 计算机上，转换器显示为大容量存储设备，允许用户安装特定的设备驱动程序。

-   如果需要使用 USSD 或多个 PDP 连接，则 IHV 必须启用该连接，并且必须符合 Windows 8、Windows 8.1 或 Windows 10 硬件认证要求。

-   你或 IHV 所需的任何其他功能必须使用设备服务扩展来实现，并且必须使用移动宽带类驱动程序和设备服务 Api 在 Windows 8、Windows 8.1 或 Windows 10 中启用。 你应在硬件要求文档中包含任何其他功能。

## <a name="span-idkey_scenariosspanspan-idkey_scenariosspanspan-idkey_scenariosspankey-scenarios"></a><span id="Key_scenarios"></span><span id="key_scenarios"></span><span id="KEY_SCENARIOS"></span>关键方案


### <a name="span-idpurchase_an_external_devicespanspan-idpurchase_an_external_devicespanspan-idpurchase_an_external_devicespanpurchase-an-external-device"></a><span id="Purchase_an_external_device"></span><span id="purchase_an_external_device"></span><span id="PURCHASE_AN_EXTERNAL_DEVICE"></span>购买外部设备

外部设备可能会在用户要开始使用之前插入。

1.  一旦插入设备，移动宽带类驱动程序就会识别并管理该设备。

2.  移动宽带服务读取 IMSI 并生成一组哈希。

3.  当用户单击 " **连接**" 时，这些哈希将用于匹配 [COSA/APN 数据库提交](cosa-apn-database-submission.md)中的连接设置。

    -   如果连接成功并且 Internet 连接可用，则无需进一步操作。 用户已购买服务。

    -   如果连接成功，但 Internet 连接不可用，则 web 浏览器将打开 APN 数据库或 UWP mobile 宽带应用中指定的 URL。

    -   如果连接失败，则会通知用户此错误。

4.  你的网站或移动宽带应用可帮助用户购买服务。

5.  购买后，通过使用预配文件中的预配 API 设置设备。 设置文件将由网站或移动宽带应用传递到预配代理。 预配文件将 Windows 配置为有关用户已购买计划的基本信息。 根据网络结构，会发生以下情况之一：

    -   用户在当前连接上被授予 Internet 访问权限。

    -   预配文件包含了断开连接并重新连接到同一网络或其他网络（将提供 Internet 访问）的说明。

### <a name="span-idconnect_an_external_device_with_an_active_simspanspan-idconnect_an_external_device_with_an_active_simspanspan-idconnect_an_external_device_with_an_active_simspanconnect-an-external-device-with-an-active-sim"></a><span id="Connect_an_external_device_with_an_active_SIM"></span><span id="connect_an_external_device_with_an_active_sim"></span><span id="CONNECT_AN_EXTERNAL_DEVICE_WITH_AN_ACTIVE_SIM"></span>使用活动的 SIM 连接外部设备

如果已将活动设备附加到已有活动的 SIM，则工作流与购买外部设备时的工作流类似，只是所尝试的连接将导致 Internet。 无需将用户定向到你的网站或移动宽带应用即可购买服务。

1.  一旦插入设备，移动宽带类驱动程序就会识别并管理该设备。

2.  移动宽带服务读取 IMSI 并生成一组哈希。

3.  当用户单击 " **连接**" 时，这些哈希将用于匹配 [COSA/APN 数据库提交](cosa-apn-database-submission.md)中的连接设置。 对于具有活动 SIM 的设备，连接成功并且 Internet 连接可用。

## <a name="span-idcomponentsspanspan-idcomponentsspanspan-idcomponentsspancomponents"></a><span id="Components"></span><span id="components"></span><span id="COMPONENTS"></span>组分


### <a name="span-idwindows_8__windows_81__or_windows_10_certified_mobile_broadband_devicesspanspan-idwindows_8__windows_81__or_windows_10_certified_mobile_broadband_devicesspanspan-idwindows_8__windows_81__or_windows_10_certified_mobile_broadband_devicesspanwindows8-windows81-or-windows10-certified-mobile-broadband-devices"></a><span id="Windows_8__Windows_8.1__or_Windows_10_certified_mobile_broadband_devices"></span><span id="windows_8__windows_8.1__or_windows_10_certified_mobile_broadband_devices"></span><span id="WINDOWS_8__WINDOWS_8.1__OR_WINDOWS_10_CERTIFIED_MOBILE_BROADBAND_DEVICES"></span>Windows 8、Windows 8.1 或已认证的 Windows 10 移动宽带设备

若要充分利用 Windows mobile 宽带平台，你的移动宽带设备必须满足 Windows 8、Windows 8.1 或 Windows 10 硬件认证要求。 有关硬件认证要求的全面说明，请参阅 [Windows 硬件认证要求](/previous-versions/windows/hardware/cert-program/)。

对于最终用户，最简化的连接体验与基于 USB 的移动宽带设备一起提供。 作为硬件认证要求的一部分，清单为 USB 设备的任何移动宽带设备都必须符合 [移动宽带接口模型 (MBIM) 规范](../network/mb-interface-model.md) 和 MBIM v1.0。 这包括外部 USB 连接器和提供 USB 接口的嵌入式模块。 对于此类设备，Windows 8、Windows 8.1 或 Windows 10 包含移动宽带类驱动程序，无需从 IHV 获取更多的驱动程序，并简化了用户的连接体验。 其他不是 USB 和驱动程序型号的硬件可以接收 Windows 8、Windows 8.1 和 Windows 10 认证，并将提供 Microsoft Store 移动宽带应用程序体验，但移动宽带类驱动程序不支持这些硬件。

### <a name="span-idmobile_broadband_class_driverspanspan-idmobile_broadband_class_driverspanspan-idmobile_broadband_class_driverspanmobile-broadband-class-driver"></a><span id="Mobile_broadband_class_driver"></span><span id="mobile_broadband_class_driver"></span><span id="MOBILE_BROADBAND_CLASS_DRIVER"></span>移动宽带类驱动程序

移动宽带类驱动程序降低了设备制造商为其特定移动宽带设备提供自定义驱动程序的负担。 移动宽带类驱动程序管理任何符合 Windows 8、Windows 8.1 或 Windows 10 设备认证的 USB MBIM 兼容移动宽带接口。 当已认证的设备连接时，无需其他驱动程序，Windows 可以立即使用该设备连接到网络。 移动宽带类驱动程序符合 Windows mobile 宽带驱动程序模型，并向 Windows Mobile 宽带服务提供完整功能。 它支持 GSM 网络，包括 HSPA + 和 LTE;CDMA 网络;和双模式网络，提供 3G CDMA 和 4G LTE。 它还支持操作员消息，如 SMS 和 USSD，以及基于 EAP SIM 的身份验证。

**注意**   尽管移动宽带类驱动程序支持 USSD、EAP-TLS 和多个 PDP 上下文，但它们是 Windows 8、Windows 8.1 或适用于桌面版的 Windows 10 () 硬件认证要求的可选组件。 但是，Windows 10 移动版需要多个 PDP 上下文进行硬件认证。

 

其他设备功能可以使用自定义设备服务扩展来实现，该扩展将通过 WinRT 设备服务 API 直接向移动宽带应用公开。

有关移动宽带类驱动程序的详细信息，请参阅 [移动宽带 (MB) 参考](/windows-hardware/drivers/ddi/_netvista/)。

### <a name="span-iddevice_service_extension_apispanspan-iddevice_service_extension_apispanspan-iddevice_service_extension_apispandevice-service-extension-api"></a><span id="Device_service_extension_API"></span><span id="device_service_extension_api"></span><span id="DEVICE_SERVICE_EXTENSION_API"></span>设备服务扩展 API

使用 Windows 平台的一个明显优势是能够提供支持运算符差异的新硬件方案。 Windows mobile 宽带平台应为可提高客户忠诚度和品牌权益的操作员启用差别。 该平台提供了一组扩展点，您可以将这些点合并到您的独特体验中。

Windows 认证的移动宽带设备将每个受支持的扩展点声明为 "设备服务"。 此类服务的示例包括电话簿、SIM 工具包或 GPS 功能。 任何未通过 Windows mobile 宽带平台本机实现的设备服务都可以使用设备服务扩展 API 进行访问。 你和 IHV 定义应该实现的设备服务。 必须同时设计 IHV 的固件和移动宽带应用以启用所需的设备服务。 USB 实现论坛正在建立适用于 [MBIMRegistry](https://www.usb.org/)的 ihv 的设备服务的注册表，并且我们建议你和你使用的 ihv 使用此注册表进行协调以确保通用设备服务扩展的一致性。

设备服务扩展 API 提供了一种直接的方法，使移动宽带应用可以在其移动宽带设备上访问功能。 这为设备提供了通过 WWAN 服务和移动宽带类驱动程序的管道，如下图所示：

![信息流过 wwan 服务](images/mbae-hwguidelines-fig1.jpg)

每个设备服务都有相应的 GUID。 在移动宽带类驱动程序与设备之间交换的所有控制消息和非 IP 数据包将携带 GUID 来标识与请求关联的服务。 命令标识符 (Cid) 并且状态指示代码在服务的 GUID 命名空间下定义。 例如，电话簿和 STK 都可以共享相同的 CID 代码，但会被在请求中交换的设备服务 GUID 区分开来。

**注意**   任何桌面应用程序或服务都可以访问基于 COM 的设备服务 API。 WinRT 投影设备服务 API 仅适用于由移动宽带操作员授权的特权 UWP 设备应用。 当以这种方式传达信息时，开发人员应认真考虑隐私和安全性。

 

Windows 无线平台支持适用于应用程序的以下功能的 Api：

-   枚举设备服务

-   打开并关闭设备服务

-   向特定设备服务发送控制命令

-   向特定设备服务发送数据或从其接收数据

-   注册来自特定设备的未经请求的设备事件

有关详细信息，请参阅 [**IMbnDeviceService 接口**](/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)。

### <a name="span-idlegacy_support_and_identity_morphingspanspan-idlegacy_support_and_identity_morphingspanspan-idlegacy_support_and_identity_morphingspanlegacy-support-and-identity-morphing"></a><span id="Legacy_support_and_identity_morphing"></span><span id="legacy_support_and_identity_morphing"></span><span id="LEGACY_SUPPORT_AND_IDENTITY_MORPHING"></span>传统支持和标识变形

Windows 8、Windows 8.1 和 Windows 10 支持为 Windows 7 设计的移动宽带设备。 尽管设备的当前生态系统将继续在 Windows 8、Windows 8.1 和 Windows 10 上运行，但它们不会充分利用 Windows 8、Windows 8.1 或 Windows 10 移动版宽带平台。

此处提供了移动宽带设备支持 Windows 8、Windows RT、Windows 8.1 和 Windows RT 8.1 的摘要：

-   Windows 10 认证设备–这些设备通过支持 Windows 10 硬件认证工具包的移动宽带体验测试。 对于这些设备，Windows 10 提供移动宽带类驱动程序和高级电源管理。

-   Windows 8 或 Windows 8.1 认证的设备–这些设备通过支持 Windows 8 或 Windows 8.1 硬件认证工具包的移动宽带体验测试。 对于这些设备，Windows 8 和 Windows 8.1 提供移动宽带类驱动程序和高级电源管理。

-   Windows 7 徽标设备-这些设备使用基于 Windows 7 NDIS 6.20 驱动程序模型的第三方 IHV 驱动程序。 Windows 8 和 Windows 8.1 提供适用于这些设备的向后兼容模式下的移动宽带体验，并限制为 Windows 7 功能。

-   与自定义连接管理器一样，windows 8 和 Windows 8.1 将继续支持旧设备，如 Windows 早期版本中所述。 Windows 8 和 Windows 8.1 将无法提供移动宽带体验，因为它们不符合移动宽带堆栈的要求。 由于移动宽带堆栈无法识别旧设备，因此通过此类设备进行连接可能会导致数据消耗过多，因为它们不是由 Windows 连接管理器管理的。

-   Windows RT 和 Windows RT 8.1 认证设备–这些设备通过 Windows RT 或 Windows RT 8.1 Windows 硬件认证工具包支持的移动宽带体验测试。 对于这些设备，Windows RT 和 Windows RT 8.1 提供移动宽带类驱动程序和高级电源管理。

    **注意**   Windows RT 和 Windows RT 8.1 系统不支持为 Windows 7 和更早版本设计的移动宽带设备。

     

为了确保 Windows 8 和 Windows 8.1 认证设备对较旧的平台很有用，Windows 提供了一个标识变形解决方案，该解决方案可让设备表现出适用于它所连接的操作系统的行为。

### <a name="span-ididentity_morphingspanspan-ididentity_morphingspanspan-ididentity_morphingspanidentity-morphing"></a><span id="Identity_morphing"></span><span id="identity_morphing"></span><span id="IDENTITY_MORPHING"></span>标识变形

当设备首次连接到 Windows 7 PC 时，典型的外部移动宽带 USB 转换器会将其自身显示为大容量存储设备。 这不会公开其他功能，以防止这些设备由于缺少驱动程序软件而显示为无法正常工作。 大容量存储设备包含 IHV 提供的软件，用于安装驱动程序包。 用户安装驱动程序包后，由 IHV 提供的软件必须对设备进行变形才能向用户公开其他功能。 此时，该设备将显示为移动宽带设备，并且用户可以连接到你的网络。

本机 Windows 8、Windows 8.1 和 Windows 10 类驱动程序消除了外部 USB 设备最初公开为大容量存储设备的需要，因为无需安装任何驱动程序。 Windows 8、Windows 8.1 和 Windows 10 包括触发设备身份变形的功能，使设备立即显示为移动宽带设备。

若要了解如何开发身份变形解决方案，请参阅 [**IMbnDeviceService 接口**](/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)。\]

### <a name="span-idfirmware_update_supportspanspan-idfirmware_update_supportspanspan-idfirmware_update_supportspanfirmware-update-support"></a><span id="Firmware_update_support"></span><span id="firmware_update_support"></span><span id="FIRMWARE_UPDATE_SUPPORT"></span>固件更新支持

应使用 Windows 更新更新移动宽带设备固件。 有关如何执行此操作的信息，请参阅 [Windows 8 上的移动宽带设备固件更新](../network/mobile-broadband-device-firmware-update.md)。 你可以使用移动宽带应用来预配你的体验的特定配置。

### <a name="span-idoma-dm_client_supportspanspan-idoma-dm_client_supportspanspan-idoma-dm_client_supportspanoma-dm-client-support"></a><span id="OMA-DM_client_support"></span><span id="oma-dm_client_support"></span><span id="OMA-DM_CLIENT_SUPPORT"></span>OMA 客户端支持

Windows 8.1 增加了对企业的 OMA 支持，以管理在 BYOD 中运行 Windows 的设备 (自带设备) 方案。 这会通过将企业相关的协议（ ([ms-MDE](https://go.microsoft.com/fwlink/?linkid=617595)、 [ms-MDM](https://go.microsoft.com/fwlink/?linkid=619346)) ）添加到这些方案中，供第三方移动设备管理提供程序和 Windows InTune 使用。

Windows 将移动网络运营商配置的 OMA 支持与企业 BYOD 的支持分隔开来。 Windows 8.1 和 Windows 10 中的 OMA 客户端不支持本机配置移动运营商特定的设置，并且不支持第三方可扩展以支持移动网络运营商要求。 支持 Windows Phone 平台的 OMA DM 解决方案与 Windows 8.1 OMA 客户端或 Windows 10 OMA 客户端不兼容。

以下是支持特定于操作员的 OMA 时要考虑的一些选项：

-   如果 OMA 客户端位于网络适配器的固件中：

    -   通常，移动宽带设备制造商可能会在其网络适配器的固件中捆绑特定于操作员的 OMA 客户端。

    -   如果不存在本机支持的解决方案，则移动宽带设备制造商可能会提供第三方的用于集成其网络适配器固件的客户端解决方案。

    -   在配置特定于操作系统的参数时，移动宽带应用应继续使用 [设置元数据](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent) 。

-   移动宽带应用中的 OMA 客户端：

    -   如果这些模块不支持网络适配器的固件中的 OMA 客户端，则可能需要在移动宽带应用中实施 OMA 客户端。

    -   此解决方案需要特定于操作员的或特定于设备制造商的自定义设备服务支持，以便通过移动宽带应用配置设备特定的参数。

    -   在配置特定于操作系统的参数时，包含 OMA 客户端的移动宽带应用应使用 [**设置元数据**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent) 。

### <a name="span-idapn_managementspanspan-idapn_managementspanspan-idapn_managementspanapn-management"></a><span id="APN_Management"></span><span id="apn_management"></span><span id="APN_MANAGEMENT"></span>APN 管理

默认 APN 管理是通过使用本地 APN 数据库来完成的。 你可能希望为有选择的用户（例如企业用户）更改接入点信息。 在这种情况下，你或 OEM 可以选择使用 OTA 信号中的 OMA DM 直接在设备上更新 APN。

设备必须实现以下各项：

-   如果在通过在该系统上使用 SIM 成功连接 **之前** 预配 by 运算符或通过 OTA 预配，则设备应将 Internet PDP 上下文作为第一个预配的上下文提供，并在由 WINDOWS 在 MBIM 节10.5.13.5 中定义时将 ContextType 设置为 **internet** 。 这可确保在尝试连接时连接逻辑使用此接入点信息。

-   如果已使用 SIM 建立了到使用该系统上的备用 APN 成功连接到网络，则将 ContextType 设置为 "Internet" 将不起作用。 强制窗口使用新接入点建立连接的唯一方法是删除创建的特定配置文件。 可以通过在提升的命令提示符下运行以下命令来删除该配置文件： **netsh mbn delete profile interface = "Mobile 宽带 Connection" name = "myProfileName"**

**注意**   由于这是一项可选的 Windows 功能，可用于支持设备，因此没有 HCK 测试或自动测试用例来验证系统上的这种情况。 我们期望操作员认证将处理验证，以确认设备符合操作员要求。

 

有关 APN 数据库的详细信息，请参阅 [apn 数据库概述](apn-database-overview.md)。

### <a name="span-idnetwork_personalizationspanspan-idnetwork_personalizationspanspan-idnetwork_personalizationspannetwork-personalization"></a><span id="Network_personalization"></span><span id="network_personalization"></span><span id="NETWORK_PERSONALIZATION"></span>网络个性化

某些操作员要求启用移动宽带的系统锁定到其网络，或要求解锁锁定的设备以允许服务可移植性。 若要启用此方案，需要 OEM 和设备供应商 \_ \_ 在 Subsidy 锁的 MBIM 规范中使用 MBIM PIN 类型指南。

设备必须在此锁定状态下报告[**WWAN \_ READY \_ INFO**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ready_info)：： [**ReadyState**](/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_ready_state) = **WwanReadyStateInitialized** ，并且不应报告**WwanReadyStateDeviceLocked**。

**注意**   没有 HCK 测试用例来验证设备或系统上实现的此功能是否适用于 Windows。 我们期待 OEM 和运营商在 MBOT 中使用特定筛选器，以确保可对最终产品进行测试。

 

 

