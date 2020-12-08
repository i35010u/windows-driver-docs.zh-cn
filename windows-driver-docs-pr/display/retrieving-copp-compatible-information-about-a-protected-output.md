---
title: 检索有关受保护输出的 COPP 兼容信息
description: 显示微型端口驱动程序可以接收请求，以检索与图形适配器的物理输出连接器关联的受保护输出的 COPP 兼容信息。
keywords:
- OPM WDK 显示，检索 COPP 兼容信息
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 17411b7878c50f3e68e70f77ffcdf7dca1846aac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799595"
---
# <a name="retrieving-copp-compatible-information-on-protected-output"></a>检索有关受保护输出的 COPP 兼容信息


显示微型端口驱动程序可以接收请求，以检索与图形适配器的物理输出连接器关联的受保护输出的 COPP 兼容信息。 显示微型端口驱动程序的 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数在包含信息请求的 *PARAMETERS* 参数中传递一个指向 [**DXGKMDT \_ OPM \_ COPP \_ 兼容 \_ GET \_ INFO \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_copp_compatible_get_info_parameters)结构的指针。 *DxgkDdiOPMGetCOPPCompatibleInformation* 将必需的信息写入 *RequestedInformation* 参数指向的 [**DXGKMDT \_ OPM \_ 请求的 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)结构。 DXGKMDT **guidInformation** **abParameters** \_ OPM \_ COPP 兼容获取信息参数的 guidInformation 和 abParameters 成员 \_ \_ \_ \_ 指定信息请求。 根据信息请求，显示微型端口驱动程序应填充 [**DXGKMDT \_ OPM \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的成员、 [**DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)、 [**DXGKMDT \_ OPM \_ ACP \_ 和 \_ CGMSA \_ 信号**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)，或 [**DXGKMDT \_ OPM \_ 连接 \_ HDCP \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)结构和所需的信息，并将 abRequestedInformation DXGKMDT **abRequestedInformation** 请求的信息指向 \_ \_ \_ 该结构。 驱动程序指定了 **cbRequestedInformationSize** (例如， <strong>sizeof (</strong>DXGKMDT \_ OPM \_ STANDARD \_ INFORMATION <strong>)</strong>) 和 **abRequestedInformation** 成员的 DXGKMDT \_ OPM 请求的 \_ \_ 信息），驱动程序必须为 OMAC DXGKMDT 请求的信息中的数据计算一个密钥密码块链接 (CBC) 模式消息身份验证代码 (OPM) \_ \_ \_ **omac** \_ \_ \_ OMAC OMAC 请求的信息。 有关计算 OMAC 的详细信息，请参阅 [OMAC 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

**注意**   在 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) 返回之前，显示微型端口驱动程序必须验证 DXGKMDT OPM COPP 兼容的 GET INFO 参数的 **ulSequenceNumber** 成员中指定的序列号是否 \_ \_ \_ \_ \_ \_ 与驱动程序当前已存储的序列号匹配。 然后，该驱动程序必须递增存储的序列号。

 

**注意**  驱动程序必须在 DXGKMDT **rnRandomNumber** \_ OPM \_ STANDARD \_ INFORMATION、DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式、DXGKMDT \_ OPM \_ ACP \_ 和 \_ CGMSA \_ 信号或 DXGKMDT \_ OPM \_ 连接 \_ HDCP \_ 设备 \_ 信息的 rnRandomNumber 成员中返回128位加密的随机数字。 随机数字是由发送应用程序生成的，在 DXGKMDT **rnRandomNumber** \_ OPM \_ COPP 兼容的 \_ \_ GET \_ INFO \_ 参数的 rnRandomNumber 成员中提供。

 

驱动程序为所指示的请求返回以下信息：

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ guidInformation 成员中设置的受支持的保护 \_ 类型，并在 DXGKMDT OPM COPP 兼容的 GET INFO 参数的 **abParameters** 成员中未定义 **guidInformation** \_ \_ \_ \_ \_ \_ ，驱动程序指示可用的保护机制类型。 为了指明可用的保护类型，驱动程序将从 DXGKMDT **ulInformation** OPM 标准信息的 ulInformation 成员中的 [**DXGKMDT \_ OPM \_ protection \_ 类型**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_protection_type)枚举中返回值的有效按位 "或" 组合 \_ \_ \_ 。 DXGKMDT \_ OPM \_ protection \_ TYPE \_ ACP、DXGKMDT \_ OPM \_ protection \_ type \_ CGMSA 和 DXGKMDT \_ OPM \_ protection \_ type \_ COPP \_ 兼容 \_ HDCP 值有效。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ 在 **GuidInformation** 中设置并在 **abParameters** 中未定义的连接器类型，驱动程序将指示连接器类型。 若要指示连接器类型，驱动程序将在 DXGKMDT **ulInformation** OPM 标准信息的 ulInformation 成员中返回值的有效按位 "或" 组合 [**\_ \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology) \_ \_ \_ 。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ 虚拟 \_ 保护 \_ 级别或 DXGKMDT \_ OPM \_ 获取 \_ \_ \_ **guidInformation** 中设置的实际保护级别和 **abParameters** 中设置的保护类型，驱动程序将在 ulInformation [**\_ DXGKMDT \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的 **OPM** 成员中返回保护级别值。 如果保护类型为 DXGKMDT \_ OPM \_ protection \_ type \_ ACP，则保护级别的值来自 [**DXGKMDT \_ OPM \_ ACP \_ protection \_ level**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level) 枚举。 如果保护类型为 DXGKMDT \_ OPM \_ protection \_ type \_ CGMSA，则保护级别的值来自 [**DXGKMDT \_ OPM \_ CGMSA**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa) 枚举。 如果保护类型为 DXGKMDT \_ OPM \_ protection \_ type \_ COPP \_ 兼容 \_ HDCP，则保护级别的值来自 [**DXGKMDT \_ OPM \_ HDCP \_ 保护 \_ 级别**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level) 枚举。

    DXGKMDT \_ OPM \_ 获取 \_ 虚拟 \_ 保护 \_ 级别请求为受保护的输出返回当前设置的保护级别。 DXGKMDT \_ OPM \_ 获取实际 \_ 的 \_ 保护 \_ 级别请求返回与受保护的输出关联的物理连接器的当前设置保护级别。

-   对于 DXGKMDT \_ OPM \_ \_ "获取 \_ \_ **guidInformation** 中的适配器总线类型" 和 "在 **abParameters** 中未定义"，驱动程序将标识将图形适配器连接到母板芯片的 "上桥" 的总线类型。 若要确定总线的类型，驱动程序将从 DXGKMDT **ulInformation** OPM 标准信息的 ulInformation 成员中的 [**DXGKMDT \_ OPM \_ bus \_ 类型 \_ 和 \_ 实现**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_bus_type_and_implementation)枚举中返回值的有效按位 "或" 组合 \_ \_ \_ 。

    此驱动程序只能将 DXGKMDT \_ OPM \_ COPP \_ 兼容 \_ 总线 \_ 类型 \_ 集成 (0x80000000) 值与其中一个总线类型值结合使用，前提是在使用公开提供的规范和标准连接器类型的扩展总线上都没有可用的接口信号。 内存总线从此定义中排除。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ \_ **guidInformation** 中设置的实际输出格式并在 **abParameters** 中未定义，驱动程序将返回 DXGKMDT 的成员中的信息，该 [**\_ \_ \_ 输出 \_ 格式**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format) 描述了如何格式化与受保护的输出关联的物理连接器的信号。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ guidInformation 中的 ACP 和 \_ CGMSA \_ 信号集并在 **abParameters** 中未定义，驱动程序将返回 **guidInformation** [**DXGKMDT \_ OPM \_ ACP \_ \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)的成员中的信息，以及描述如何保护通过与受保护的输出关联的物理连接器的信号的信号。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ guidInformation 中的已连接 \_ hdcp \_ 设备 \_ 信息集并在 **abParameters** 中未定义，驱动程序将在 [**DXGKMDT \_ OPM \_ 连接的 \_ hdcp \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)的成员中返回信息，其中包含高带宽数字内容保护 (HDCP) 信息。 **guidInformation**

 

