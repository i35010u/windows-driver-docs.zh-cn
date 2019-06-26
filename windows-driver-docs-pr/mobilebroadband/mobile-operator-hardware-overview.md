---
title: 移动运营商硬件概述
description: 移动运营商硬件概述
ms.assetid: b2322972-16be-443f-b46a-7834b4d7ead0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4214393f781662e11d8ace8fdb07567be94fd9e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393423"
---
# <a name="mobile-operator-hardware-overview"></a>移动运营商硬件概述


应使用本主题以获取 Windows 8、 Windows 8.1 和 Windows 10 的移动宽带硬件要求和建议的高层次了解。 我们建议以下内容以提供简化连接与客户体验以及减少您的维护和支持成本。

-   嵌入移动宽带模块，提供 USB 接口必须满足 Windows 8、 Windows 8.1 或 Windows 10 硬件认证要求，并且通过使用移动宽带类驱动程序进行管理。 硬件要求文档 ihv 应要求移动宽带设备，将传递给 Windows 8、 Windows 8.1 或 Windows 10 设备认证。

-   外部 USB 移动宽带连接器必须支持标识变形。 硬件要求文档 ihv 应要求外部移动宽带设备传递的 Windows 8 设备认证，Windows 8.1 或 Windows 10 设备认证，并通过 Windows 7 徽标认证。

    -   在 Windows 10 计算机，硬件保护装置显示为认证移动宽带设备对 Windows 10，并使用移动宽带类驱动程序进行管理。

    -   Windows 8.1 计算机上硬件保护装置显示为 Windows 8.1 认证移动宽带设备，并使用移动宽带类驱动程序进行管理。

    -   Windows 8 计算机上，硬件保护装置显示为 Windows 8 认证移动宽带设备，并使用移动宽带类驱动程序进行管理。

    -   在 Windows 7 计算机硬件保护装置显示为大容量存储设备，允许用户安装特定设备驱动程序。

-   如果您需要 EAP-SIM、 USSD 或多个 PDP 连接，IHV 必须启用它并且它必须符合 Windows 8、 Windows 8.1 或 Windows 10 硬件认证要求。

-   使用设备服务扩展和使用移动宽带类驱动程序和设备服务 Api 在 Windows 8、 Windows 8.1 或 Windows 10 中启用，则必须实现您或 IHV 所需的任何其他功能。 应包括任何其他功能作为您的硬件要求文档的一部分。

## <a name="span-idkeyscenariosspanspan-idkeyscenariosspanspan-idkeyscenariosspankey-scenarios"></a><span id="Key_scenarios"></span><span id="key_scenarios"></span><span id="KEY_SCENARIOS"></span>关键方案


### <a name="span-idpurchaseanexternaldevicespanspan-idpurchaseanexternaldevicespanspan-idpurchaseanexternaldevicespanpurchase-an-external-device"></a><span id="Purchase_an_external_device"></span><span id="purchase_an_external_device"></span><span id="PURCHASE_AN_EXTERNAL_DEVICE"></span>购买外部设备

外部设备很可能要插入之前用户想要开始使用它。

1.  只要插入设备时，它的识别和管理移动宽带类驱动程序。

2.  移动宽带服务读取 IMSI 并生成一系列哈希值。

3.  当用户单击**Connect**，这些哈希将用于匹配中的连接设置[COSA/APN 数据库提交](cosa-apn-database-submission.md)。

    -   如果连接成功和 Internet 连接可用，不会执行任何进一步操作。 用户已购买了服务。

    -   如果连接成功，但是 Internet 连接不可用，web 浏览器将打开 APN 数据库或 UWP 移动宽带应用程序中指定的 URL。

    -   如果连接失败，错误的通知用户。

4.  你的网站或移动宽带应用可帮助用户购买的服务。

5.  购买后, 从预配文件使用预配 API 设置设备。 在网站或移动宽带应用预配文件被传递给预配的代理。 预配文件配置 Windows 用户已购买的计划有关的基本信息。 根据网络结构中，将发生以下情况之一：

    -   用户被授予当前连接上的 Internet 访问。

    -   预配文件包括断开连接，然后重新连接到同一网络或其他网络，它将提供 Internet 访问权限的说明。

### <a name="span-idconnectanexternaldevicewithanactivesimspanspan-idconnectanexternaldevicewithanactivesimspanspan-idconnectanexternaldevicewithanactivesimspanconnect-an-external-device-with-an-active-sim"></a><span id="Connect_an_external_device_with_an_active_SIM"></span><span id="connect_an_external_device_with_an_active_sim"></span><span id="CONNECT_AN_EXTERNAL_DEVICE_WITH_AN_ACTIVE_SIM"></span>使用 active SIM 连接外部设备

活动设备附加已 active SIM，工作流将类似于当您购买外部设备，不同之处在于所尝试的连接将会导致连接到 Internet。 您不必将用户定向到你的网站或移动宽带应用购买服务。

1.  只要插入设备时，它的识别和管理移动宽带类驱动程序。

2.  移动宽带服务读取 IMSI 并生成一系列哈希值。

3.  当用户单击**Connect**，这些哈希将用于匹配中的连接设置[COSA/APN 数据库提交](cosa-apn-database-submission.md)。 具有活动 SIM 的设备，连接成功和 Internet 连接可用。

## <a name="span-idcomponentsspanspan-idcomponentsspanspan-idcomponentsspancomponents"></a><span id="Components"></span><span id="components"></span><span id="COMPONENTS"></span>组件


### <a name="span-idwindows8windows81orwindows10certifiedmobilebroadbanddevicesspanspan-idwindows8windows81orwindows10certifiedmobilebroadbanddevicesspanspan-idwindows8windows81orwindows10certifiedmobilebroadbanddevicesspanwindows8-windows81-or-windows10-certified-mobile-broadband-devices"></a><span id="Windows_8__Windows_8.1__or_Windows_10_certified_mobile_broadband_devices"></span><span id="windows_8__windows_8.1__or_windows_10_certified_mobile_broadband_devices"></span><span id="WINDOWS_8__WINDOWS_8.1__OR_WINDOWS_10_CERTIFIED_MOBILE_BROADBAND_DEVICES"></span>Windows 8、 Windows 8.1 或 Windows 10 认证移动宽带设备

若要充分利用 Windows 移动宽带平台，你的移动宽带设备必须满足 Windows 8、 Windows 8.1 或 Windows 10 硬件认证要求。 有关硬件认证要求的全面描述，请参阅[Windows 硬件认证要求](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/)。

为最终用户的最简单的连接体验传递与基于 USB 的移动宽带设备。 硬件认证要求的一部分，任何表现为 USB 设备的移动宽带设备必须符合[移动宽带接口模型 (MBIM) 规范](https://docs.microsoft.com/windows-hardware/drivers/network/mb-interface-model)和 MBIM v1.0 勘误表。 这包括外部 USB 连接器和嵌入的模块，提供 USB 接口。 对于此类设备，Windows 8、 Windows 8.1 或 Windows 10 包括移动宽带类驱动程序，它不需要其他驱动程序 ihv 和简化了用户的连接体验。 不是 USB 和驱动程序模型的其他硬件可以接收 Windows 8、 Windows 8.1 和 Windows 10 证书并将提供在 Microsoft Store 的移动宽带应用体验，但这些不受移动宽带类驱动程序。

### <a name="span-idmobilebroadbandclassdriverspanspan-idmobilebroadbandclassdriverspanspan-idmobilebroadbandclassdriverspanmobile-broadband-class-driver"></a><span id="Mobile_broadband_class_driver"></span><span id="mobile_broadband_class_driver"></span><span id="MOBILE_BROADBAND_CLASS_DRIVER"></span>移动宽带类驱动程序

移动宽带类驱动程序减少了设备制造商提供其特定的移动宽带设备的自定义驱动程序的负担。 移动宽带类驱动程序管理的 Windows 8、 Windows 8.1 或 Windows 10 设备认证满足任何符合 USB MBIM 的移动宽带接口。 当已认证的设备连接时，没有其他驱动程序所需和 Windows 可以立即使用该设备以连接到网络。 移动宽带类驱动程序符合 Windows 移动宽带的驱动程序模型，并为 Windows 移动宽带服务提供了完整的功能。 它支持 GSM 网络，包括 HSPA + 和 LTE;CDMA 网络;而且双模式网络产品/服务 3 的 G CDMA 和 4g LTE。 它还支持运算符消息，如 SMS 和 USSD 和基于 EAP 的 SIM 身份验证。

**请注意**  时 USSD、 EAP SIM 和多个 PDP 上下文支持的移动宽带类驱动程序，它们是可选组件的 Windows 8、 Windows 8.1 或 Windows 10 桌面版 (主页、 专业版、 企业版、 和教育） 硬件认证要求。 但是，多个 PDP 上下文所需适用于 Windows 10 移动设备硬件认证。

 

可以使用自定义设备服务扩展，将直接向通过 WinRT 设备服务 API 的移动宽带应用公开实现其他设备功能。

移动宽带类驱动程序的详细信息，请参阅[移动宽带 (MB) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

### <a name="span-iddeviceserviceextensionapispanspan-iddeviceserviceextensionapispanspan-iddeviceserviceextensionapispandevice-service-extension-api"></a><span id="Device_service_extension_API"></span><span id="device_service_extension_api"></span><span id="DEVICE_SERVICE_EXTENSION_API"></span>设备服务扩展 API

使用 Windows 平台的明显的优势之一是能够提供支持运算符区分的新硬件情况。 Windows 移动宽带平台需要实现更高版本的客户忠诚度和品牌权益可以命令的运算符的优势。 平台提供了一组可以合并到你独特的体验的扩展点。

Windows 认证的移动宽带设备声明为"设备服务"每个受支持的扩展点。 此类服务的示例包括通讯簿、 SIM 工具包或 GPS 功能。 可以通过使用设备服务扩展 API 访问不由 Windows 移动宽带平台本机实现的任何设备服务。 您和 IHV 定义应实现的设备服务。 IHV 的固件和移动宽带应用程序必须能够同时启用所需的设备的服务。 USB 实现论坛建立一个可供在 Ihv 的设备服务注册表[MBIMRegistry](https://www.usb.org/)，我们建议您和您正在使用 Ihv 使用此注册表进行协调以确保一致性和常见的设备服务扩展插件。

设备服务扩展 API 提供移动宽带应用程序访问其移动宽带设备上的功能的直接方法。 这提供了通过 WWAN 服务和设备的移动宽带类驱动程序的管道，如以下关系图中所示：

![信息流通过 wwan 服务](images/mbae-hwguidelines-fig1.jpg)

每个设备服务都有一个相应的 GUID。 所有控制消息和移动宽带类驱动程序和设备之间交换的非 IP 数据包将都附带 GUID 来标识与请求关联的服务。 服务的 GUID 命名空间下定义的命令标识符 (Cid) 和状态指示代码。 例如，通讯簿和 STK 可以共享相同的 CID 代码，但将通过设备服务在请求中交换的 GUID 进行区分。

**请注意**  基于 COM 的设备服务 API 是可供任何桌面应用程序或服务访问。 WinRT 投影的设备服务 API 是仅供通过移动宽带运营商进行授权的特权 UWP 设备应用程序。 开发人员应仔细考虑隐私和安全通信通过这种方式的信息时。

 

Windows 无线平台支持的 Api 适用于应用的以下功能：

-   枚举设备的服务

-   打开和关闭设备服务

-   将控制命令发送到特定设备服务

-   发送或接收数据到或从特定设备服务

-   注册，以便从特定设备的未经请求的设备事件

有关详细信息，请参阅[ **IMbnDeviceService 接口**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)。

### <a name="span-idlegacysupportandidentitymorphingspanspan-idlegacysupportandidentitymorphingspanspan-idlegacysupportandidentitymorphingspanlegacy-support-and-identity-morphing"></a><span id="Legacy_support_and_identity_morphing"></span><span id="legacy_support_and_identity_morphing"></span><span id="LEGACY_SUPPORT_AND_IDENTITY_MORPHING"></span>旧版支持和标识变形

Windows 8、 Windows 8.1 和 Windows 10 支持为 Windows 7 设计的移动宽带设备。 设备的当前生态系统仍可在 Windows 8、 Windows 8.1 和 Windows 10 上正常工作而他们无法充分利用 Windows 8、 Windows 8.1 或 Windows 10 的移动宽带平台。

此处提供的移动宽带设备支持以外 8，Windows RT、 Windows 8.1 和 Windows RT 8.1 的摘要：

-   Windows 10 已认证设备 – 这些设备通过支持 Windows 10 硬件认证工具包的移动宽带体验测试。 对于这些设备，Windows 10 提供了移动宽带类驱动程序和高级电源管理。

-   Windows 8 或 Windows 8.1 已认证设备 – 这些设备通过支持 Windows 8 或 Windows 8.1 硬件认证工具包的移动宽带体验测试。 对于这些设备，Windows 8 和 Windows 8.1 提供移动宽带类驱动程序和高级电源管理。

-   获得 Windows 7 徽标的设备 – 这些设备使用基于 Windows 7 NDIS 6.20 驱动程序模型的第三方 IHV 驱动程序。 Windows 8 和 Windows 8.1 为这些设备提供移动宽带体验在向后兼容性模式下，它们仅限于 Windows 7 功能。

-   Windows 8 和 Windows 8.1 将继续支持基于调制解调器或以太网接口以及与早期版本的 Windows 的自定义连接管理器的旧设备。 Windows 8 和 Windows 8.1 将不能提供移动宽带体验不符合移动宽带堆栈。 旧的设备无法识别的移动宽带堆栈，因为通过此类设备建立连接可能会导致数据过度使用因为它们不托管的 Windows 连接管理器。

-   Windows RT 和 Windows RT 8.1 已认证设备 – 这些设备通过 Windows RT 或 Windows RT 8.1 Windows 硬件认证工具包支持的移动宽带体验测试。 对于这些设备，Windows RT 和 Windows RT 8.1 提供移动宽带类驱动程序和高级电源管理。

    **请注意**   Windows RT 和 Windows RT 8.1 的系统不支持用于 Windows 7 及更早版本的移动宽带设备。

     

若要确保 Windows 8 和 Windows 8.1 已认证设备在较旧的平台上很有用，Windows 提供了标识变形解决方案，使设备以显示适用于连接到的操作系统的行为。

### <a name="span-ididentitymorphingspanspan-ididentitymorphingspanspan-ididentitymorphingspanidentity-morphing"></a><span id="Identity_morphing"></span><span id="identity_morphing"></span><span id="IDENTITY_MORPHING"></span>标识变形

当设备首次连接到 Windows 7 PC 时，典型外部的移动宽带 USB 转换器将自己呈现为大容量存储设备。 这不公开其他功能，若要阻止这些设备显示为非功能性由于缺少驱动程序软件。 大容量存储设备包含安装驱动程序包的 IHV 提供软件。 用户安装的驱动程序包后，IHV 提供软件必须执行 morph 以公开给用户的其他函数的设备。 此时，设备将显示为移动宽带设备，用户可以连接到网络。

在本机 Windows 8、 Windows 8.1 和 Windows 10 类驱动程序不需要公开自身最初为大容量存储设备，因为没有安装驱动程序是必需的外部 USB 设备。 Windows 8、 Windows 8.1 和 Windows 10 包括触发设备的标识变形和允许的设备将立即显示为移动宽带设备的功能。

若要了解如何开发变形解决方案的标识，请参阅[ **IMbnDeviceService 接口**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)。\]

### <a name="span-idfirmwareupdatesupportspanspan-idfirmwareupdatesupportspanspan-idfirmwareupdatesupportspanfirmware-update-support"></a><span id="Firmware_update_support"></span><span id="firmware_update_support"></span><span id="FIRMWARE_UPDATE_SUPPORT"></span>固件更新支持

应使用 Windows Update 更新移动宽带设备固件。 有关如何执行此操作的信息，请参见[移动宽带设备固件更新，在 Windows 8 上](https://docs.microsoft.com/windows-hardware/drivers/network/mobile-broadband-device-firmware-update)。 可以通过使用移动宽带应用预配你的体验针对特定的配置。

### <a name="span-idoma-dmclientsupportspanspan-idoma-dmclientsupportspanspan-idoma-dmclientsupportspanoma-dm-client-support"></a><span id="OMA-DM_client_support"></span><span id="oma-dm_client_support"></span><span id="OMA-DM_CLIENT_SUPPORT"></span>OMA DM 客户端支持

Windows 8.1 添加了适用于企业管理 BYOD （自带设备办公） 方案中运行 Windows 的设备的 OMA DM 支持。 该命令对这些方案的支持扩展通过添加相关企业协议 ([MS MDE](https://go.microsoft.com/fwlink/?linkid=617595)， [MS MDM](https://go.microsoft.com/fwlink/?linkid=619346)) 以供第三方移动设备管理提供程序和 Windows InTune。

Windows 将从企业 BYOD 的支持的移动网络运算符配置 OMA DM 支持分隔开来。 在 Windows 8.1 和 Windows 10 OMA DM 客户端不支持配置移动操作员特定设置本机和是不第三方可扩展以支持移动网络运算符要求。 OMA DM 解决方案支持 Windows Phone 平台不与 Windows 8.1 的 OMA-DM 客户端或 Windows 10 OMA DM 客户端兼容。

下面是一些选项，以支持特定于运算符的 OMA DM 时，请考虑：

-   如果 OMA DM 客户端网络适配器的固件中：

    -   通常情况下，移动宽带设备制造商可能在其网络适配器的固件中捆绑特定于运算符的 OMA DM 客户端。

    -   移动宽带设备制造商可能能够提供第三方 OMA DM 客户端解决方案集成在其网络适配器固件中，如果本机支持的解决方案不存在。

    -   移动宽带应用程序应继续使用[预配的元数据](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)配置操作系统特定的参数时。

-   OMA DM 客户端的移动宽带应用中：

    -   如果模块不支持网络适配器的固件中的 OMA DM 客户端，可能想要移动的宽带应用程序中实现 OMA DM 客户端。

    -   此解决方案配置设备特定参数的移动宽带应用程序需要特定于运算符的或设备制造商特定于自定义设备服务支持。

    -   包括的 OMA DM 客户端的移动宽带应用应使用[**预配的元数据**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)配置操作系统特定的参数时。

### <a name="span-idapnmanagementspanspan-idapnmanagementspanspan-idapnmanagementspanapn-management"></a><span id="APN_Management"></span><span id="apn_management"></span><span id="APN_MANAGEMENT"></span>APN 管理

默认 APN 管理可通过使用本地的 APN 数据库。 您可能想要在更改对于选择性的用户，如企业用户的 APN 信息。 在这种情况下，您或 OEM 可以选择直接在设备上的 APN 使用更新的 OMA DM 中 OTA 信号。

你的设备必须实现以下功能：

-   当预配了运算符或通过 OTA 预配**早于**成功连接时在该系统上使用 SIM，如具有 ContextType 的第一个预配的上下文设置为，设备应提供 Internet PDP 上下文**Internet** MBIM 10.5.13.5 一节中定义 Windows 进行查询时。 这可以确保连接逻辑尝试连接时使用此 APN 的信息。

-   如果 SIM 用于建立成功连接到该系统上使用备用 APN 的网络，向 Internet 设置 ContextType 不起作用。 强制该窗口以使用新的 APN 建立连接的唯一方法是删除创建的特定配置文件。 可以通过从提升的命令提示符运行以下命令来删除该配置文件： **netsh mbn 删除配置文件接口 ="移动宽带连接"名称 ="myProfileName"**

**请注意**  由于这是设备，以支持的可选 Windows 功能，没有 HCK 测试或自动的测试用例来验证这种情况下，在系统上的。 运算符认证将处理验证以确认设备符合运算符要求我们期望它。

 

APN 数据库有关的详细信息，请参阅[APN 数据库概述](apn-database-overview.md)。

### <a name="span-idnetworkpersonalizationspanspan-idnetworkpersonalizationspanspan-idnetworkpersonalizationspannetwork-personalization"></a><span id="Network_personalization"></span><span id="network_personalization"></span><span id="NETWORK_PERSONALIZATION"></span>网络个性化设置

某些运算符需要移动宽带启用系统被锁定到其网络或已解锁锁定的设备以允许服务可移植性的要求。 若要启用此方案中，我们要求的 OEM 和设备供应商使用 MBIM\_PIN\_Subsidy 锁类型 MBIM 规范中的指南。

设备必须报告[ **WWAN\_准备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ready_info)::[**ReadyState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ne-wwan-_wwan_ready_state)=**WwanReadyStateInitialized**在此锁定状态，不应报告**WwanReadyStateDeviceLocked**。

**请注意**  没有 HCK 测试用例，以验证在设备上实现此功能，或者系统适用于 Windows。 我们向 OEM 和运算符使用 MBOT 中的特定筛选器以确保最终产品可以进行测试。

 

 

 





