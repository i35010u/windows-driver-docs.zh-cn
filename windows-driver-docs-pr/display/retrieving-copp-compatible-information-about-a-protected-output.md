---
title: 检索有关受保护输出的 COPP 兼容信息
description: 显示微型端口驱动程序可以接收请求，以检索与图形适配器的物理输出连接器关联的受保护输出的 COPP 兼容信息。
ms.assetid: 9114f232-4123-47a8-b43d-62d14b9f6b08
keywords:
- OPM WDK 显示，检索 COPP 兼容信息
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 0e74c2c8a5f6118c356f36d8d0fd5a2293c65bd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825834"
---
# <a name="retrieving-copp-compatible-information-on-protected-output"></a>检索有关受保护输出的 COPP 兼容信息


显示微型端口驱动程序可以接收请求，以检索与图形适配器的物理输出连接器关联的受保护输出的 COPP 兼容信息。 显示微型端口驱动程序的[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数将被传递到[**DXGKMDT\_OPM\_COPP\_兼容的指针\_获取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_copp_compatible_get_info_parameters)*参数*参数中包含信息请求的\_信息\_参数结构。 *DxgkDdiOPMGetCOPPCompatibleInformation*会将所需的信息写入\_*RequestedInformation*参数所指向的[**信息结构\_\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information) 。 DXGKMDT\_OPM\_COPP 的**guidInformation**和**ABPARAMETERS**成员\_兼容\_获取\_INFO\_参数指定信息请求。 根据信息请求，显示微型端口驱动程序应填充[**DXGKMDT\_OPM 的成员\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)、 [**DXGKMDT\_OPM\_实际\_输出\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)、 [**DXGKMDT\_OPM\_ACP\_和\_CGMSA\_信号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)，或[**DXGKMDT\_OPM\_连接\_HDCP\_设备\_的信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)结构信息，并将 DXGKMDT\_OPM 的**abRequestedInformation**成员指向该结构\_请求\_的信息。 当驱动程序指定**cbRequestedInformationSize** （例如， <strong>sizeof （</strong>DXGKMDT\_OPM\_标准\_信息<strong>）</strong>）并**abRequestedInformation**成员 DXGKMDT\_OPM\_请求的\_信息时，驱动程序必须为 OMAC 中的数据计算一个密钥密码块链（CBC）模式消息身份验证代码（DXGKMDT）（OPM），并**在**DXGKMDT\_OPM 的 omac 成员\_请求\_的信息。\_\_\_ 有关计算 OMAC 的详细信息，请参阅[OMAC 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

**注意**   在[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)返回之前，显示微型端口驱动程序必须验证 DXGKMDT\_OPM\_COPP\_兼容\_的**ulSequenceNumber**成员中指定的序列号是否兼容\_获取\_的信息的参数是否与当前已存储的驱动程序序列号匹配。 然后，该驱动程序必须递增存储的序列号。

 

**请注意**   驱动程序必须在 DXGKMDT\_OPM 的**rnRandomNumber**成员中返回128位加密的安全随机数\_标准\_信息、DXGKMDT\_OPM\_实际\_输出\_格式、DXGKMDT\_OPM\_ACP\_和\_CGMSA\_\_\_\_\_\_ 随机数字是由发送应用程序生成的，并在 DXGKMDT\_OPM\_COPP\_兼容\_获取\_INFO\_参数的**rnRandomNumber**成员中提供。

 

驱动程序为所指示的请求返回以下信息：

-   对于 DXGKMDT\_OPM\_获取在**guidInformation**成员中**设置的\_** \_保护\_类型，在 DXGKMDT\_OPM\_COPP\_兼容\_获取\_INFO\_参数中未定义，驱动程序指示可用的保护机制类型。 为了指明可用的保护类型，驱动程序将返回\_DXGKMDT 中的值的有效按位 "或" 组合[ **\_保护\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_protection_type)枚举中的**ulInformation**成员 DXGKMDT\_OPM\_标准\_信息。 DXGKMDT\_OPM\_保护\_类型\_ACP、DXGKMDT\_OPM\_保护\_类型\_CGMSA 和 DXGKMDT\_OPM\_保护\_类型\_COPP\_兼容\_HDCP 值有效。

-   对于 DXGKMDT\_OPM\_获取**guidInformation**中设置的\_连接器\_类型，并在**abParameters**中定义，驱动程序指示连接器类型。 为了指示连接器类型，驱动程序将从[**D3DKMDT\_视频\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)中返回值的有效按位 "或" 组合，\_DXGKMDT\_OPM\_标准\_信息的**ulInformation**成员中。

-   对于 DXGKMDT\_OPM\_获取\_虚拟\_保护\_LEVEL 或 DXGKMDT\_OPM\_获取在**guidInformation**中设置\_实际\_保护\_级别，在 abParameters 中设置**保护类型，驱动**程序将在 ULINFORMATION [ **\_DXGKMDT\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的**OPM**成员中返回一个保护级别值。 如果保护类型为 DXGKMDT\_OPM\_保护\_类型\_ACP，则保护级别的值来自[**DXGKMDT\_OPM\_ACP\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)枚举。\_ 如果保护类型为 DXGKMDT\_OPM\_保护\_类型\_CGMSA，则保护级别的值来自[**DXGKMDT\_OPM\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)枚举。 如果保护类型为 DXGKMDT\_OPM\_PROTECTION\_类型\_COPP\_兼容\_HDCP，则保护级别值来自[**DXGKMDT\_OPM\_hdcp\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)枚举。\_

    DXGKMDT\_OPM\_获取\_虚拟\_保护\_LEVEL 请求为受保护的输出返回当前设置的保护级别。 DXGKMDT\_OPM\_获取\_实际\_保护\_LEVEL 请求为与受保护的输出关联的物理连接器返回当前设置的保护级别。

-   对于 DXGKMDT\_OPM\_获取在**guidInformation**中设置的\_适配器\_总线\_类型，并在**abParameters**中定义，驱动程序将标识将图形适配器连接到主板芯片的上桥的总线类型。 若要确定总线的类型，驱动程序将返回[**DXGKMDT\_OPM\_总线\_类型\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_bus_type_and_implementation)中的值的有效按位 "或" 组合，并在 DXGKMDT\_OPM\_标准\_信息的**ulInformation**成员中\_实现枚举。

    此驱动程序只能将 DXGKMDT\_OPM\_COPP\_兼容\_总线\_类型\_集成（0x80000000）值与其中一个总线类型值结合使用，前提是在使用公开提供的规范和标准连接器类型的扩展总线上没有可用的接口信号。 内存总线从此定义中排除。

-   对于 DXGKMDT\_OPM\_在**guidInformation**中获取\_实际\_输出\_格式，在**abParameters**中未定义，驱动程序将返回 DXGKMDT\_OPM 的成员中的信息\_[**实际\_输出\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)，描述如何格式化与受保护的输出关联的物理连接器的信号。

-   对于 DXGKMDT\_OPM\_获取\_ACP\_，\_CGMSA\_**guidInformation 中设置的、** abParameters 中未定义的**信号，驱动**程序将返回 DXGKMDT\_OPM\_ACP\_[**和\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)的成员中的信息，并说明如何保护通过与受保护的输出关联的物理连接器的信号。\_

-   对于 DXGKMDT\_OPM\_获取\_连接\_HDCP\_设备\_在**guidInformation**中设置的信息，并在**abParameters**中未定义，驱动程序将返回[**DXGKMDT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)\_\_\_\_\_内容保护

 

 





