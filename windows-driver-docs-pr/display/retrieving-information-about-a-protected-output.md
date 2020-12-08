---
title: 检索有关受保护输出的信息
description: 检索有关受保护输出的信息
keywords:
- OPM WDK 显示，检索受保护的输出信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7989cd12b7fc278fe383df895cbceb6138919ba4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824199"
---
# <a name="retrieving-information-about-a-protected-output"></a>检索有关受保护输出的信息


显示微型端口驱动程序可以接收请求，以检索与图形适配器的物理输出连接器关联的受保护输出的相关信息。 显示微型端口驱动程序的 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)函数在包含信息请求的 *PARAMETERS* 参数中传递一个指向 [**DXGKMDT \_ OPM \_ GET \_ INFO \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)结构的指针。 *DxgkDdiOPMGetInformation* 将必需的信息写入 *RequestedInformation* 参数指向的 [**DXGKMDT \_ OPM \_ 请求的 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)结构。 DXGKMDT OPM GET INFO 参数的 **guidInformation** 和 **abParameters** 成员 \_ \_ \_ \_ 指定信息请求。 根据信息请求，显示微型端口驱动程序应该用所需的信息填充 [**DXGKMDT \_ OPM \_ STANDARD \_ information**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)、 [**DXGKMDT \_ OPM \_ OUTPUT \_ ID**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)或 [**DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format) 结构的成员，并将 abRequestedInformation DXGKMDT 请求信息的 **OPM** 成员 \_ 指向 \_ \_ 该结构。 当驱动程序指定 **cbRequestedInformationSize** (例如，SIZEOF (DXGKMDT \_ OPM \_ 标准 \_ 信息) # A3 和 **abRequestedInformation** 成员的 DXGKMDT \_ OPM 请求的 \_ \_ 信息），驱动程序必须为 OMAC DXGKMDT 请求的信息中的数据 (CBC) 模式消息身份验证代码 (OPM) 计算一个密钥密码块链 \_ \_ \_ ，并必须在 OMAC OMAC 请求的信息的 **DXGKMDT** 成员中设置此 OPM \_ \_ \_ 。 有关计算 OMAC 的详细信息，请参阅 [OMAC 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

**注意**   在 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information) 返回之前，显示微型端口驱动程序必须验证在 DXGKMDT OPM 的 **OMAC** 成员中指定的 [**OMAC \_ \_ 获取 \_ 信息 \_ 参数**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters) 是否正确。 驱动程序还必须验证在 DXGKMDT OPM 获取 INFO 参数的 **ulSequenceNumber** 成员中指定的序列号是否 \_ \_ \_ \_ 与驱动程序当前已存储的序列号匹配。 然后，该驱动程序必须递增存储的序列号。

 

**注意**  驱动程序必须在 DXGKMDT **rnRandomNumber** \_ OPM \_ STANDARD \_ INFORMATION、 [**DXGKMDT \_ OPM \_ OUTPUT \_ ID**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)或 DXGKMDT \_ OPM \_ 实际 \_ 输出 \_ 格式的 rnRandomNumber 成员中返回128位加密的随机数字。 随机数字是由发送应用程序生成的，并在 DXGKMDT **rnRandomNumber** \_ OPM \_ GET \_ INFO \_ 参数的 rnRandomNumber 成员中提供。

 

驱动程序为所指示的请求返回以下信息：

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ guidInformation 成员中设置的受支持的保护 \_ 类型，并在 DXGKMDT OPM GET INFO 参数结构的 **abParameters** 成员中未定义 **guidInformation** \_ \_ \_ \_ ，驱动程序指示可用的保护机制类型。 为了指明可用的保护类型，驱动程序将从 DXGKMDT **ulInformation** OPM 标准信息的 ulInformation 成员中的 [**DXGKMDT \_ OPM \_ protection \_ 类型**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_protection_type)枚举中返回值的有效按位 "或" 组合 \_ \_ \_ 。 DXGKMDT \_ OPM \_ protection \_ 类型 \_ HDCP 和 DXGKMDT \_ OPM \_ protection \_ type \_ DPCP 值有效。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ 在 **GuidInformation** 中设置并在 **abParameters** 中未定义的连接器类型，驱动程序将指示连接器类型。 若要指示连接器类型，驱动程序将在 DXGKMDT **ulInformation** OPM 标准信息的 ulInformation 成员中返回值的有效按位 "或" 组合 [**\_ \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology) \_ \_ \_ 。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ 虚拟 \_ 保护 \_ 级别或 DXGKMDT \_ OPM \_ 获取 \_ \_ \_ **guidInformation** 中设置的实际保护级别和 **abParameters** 中设置的保护类型，驱动程序将在 ulInformation [**\_ DXGKMDT \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的 **OPM** 成员中返回保护级别值。 如果保护类型为 DXGKMDT \_ OPM \_ protection \_ type \_ HDCP，则保护级别的值来自 [**DXGKMDT \_ OPM \_ HDCP \_ 保护 \_ 级别**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level) 枚举。 如果保护类型为 DXGKMDT \_ OPM \_ protection \_ type \_ DPCP，则保护级别的值来自 [**DXGKMDT \_ OPM \_ DPCP \_ protection \_ level**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level) 枚举。

    DXGKMDT \_ OPM \_ 获取 \_ 虚拟 \_ 保护 \_ 级别请求为受保护的输出返回当前设置的保护级别。 DXGKMDT \_ OPM \_ 获取实际 \_ 的 \_ 保护 \_ 级别请求返回与受保护的输出关联的物理连接器的当前设置保护级别。

-   对于 DXGKMDT \_ OPM \_ \_ "获取 \_ \_ **guidInformation** 中的适配器总线类型" 和 "在 **abParameters** 中未定义"，驱动程序将标识将图形适配器连接到母板芯片的 "bridge" 的总线的类型和实现。 若要确定总线的类型和实现，驱动程序将从 DXGKMDT **ulInformation** OPM 标准信息的 ulInformation 成员中的 [**DXGKMDT \_ OPM \_ bus \_ 类型 \_ 和 \_ 实现**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_bus_type_and_implementation)枚举中返回值的有效按位 "或" 组合 \_ \_ \_ 。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ guidInformation 中的当前 HDCP \_ SRM \_ 版本集并在 **abParameters** 中未定义，驱动程序将在 ulInformation [**\_ DXGKMDT \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的 **OPM** 成员中返回一个值，该信息标识当前高带宽数字内容保护 (HDCP) 系统 Renewability 消息 (SRM) 用于受保护的输出。 **guidInformation** 最小有效位 (位0到 15) 包含以小字节序格式表示的 SRM 版本号。 有关 SRM 版本号的详细信息，请参阅 [HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ \_ **guidInformation** 中设置的实际输出格式并在 **abParameters** 中未定义，驱动程序将返回 DXGKMDT 的成员中的信息，该 [**\_ \_ \_ 输出 \_ 格式**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format) 描述了如何格式化与受保护的输出关联的物理连接器的信号。

-   对于 DXGKMDT \_ OPM \_ GET \_ \_ **guidInformation** 中设置的输出 id 并在 **abParameters** 中未定义，驱动程序将返回标识输出连接器的 [**DXGKMDT \_ OPM \_ 输出 \_ ID**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id) 成员的信息。

-   对于 DXGKMDT \_ OPM \_ 获取 \_ \_ **guidInformation** 成员中设置的 DVI 特征，并在 DXGKMDT OPM 获取信息参数结构的 **abParameters** 成员中未定义 \_ \_ \_ \_ ，驱动程序指示数字视频接口 (DVI) 输出连接器的电气特征。 为了指明 DVI 电气特征，驱动程序从 [**DXGKMDT \_ OPM \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的 **ulInformation** 成员的 [**DXGKDT \_ OPM \_ DVI \_ 特征**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkdt_opm_dvi_characteristics)枚举中返回一个值。

 

