---
title: 使用 OPM DDI
description: 使用 OPM DDI
ms.assetid: cd3c78a4-0241-48ab-9005-c544db199eb5
keywords:
- OPM WDK 显示，关于 DDI
- OPM WDK 显示，创建受保护的输出
- OPM WDK 显示，销毁受保护的输出
- OPM WDK 显示，获取证书
- OPM WDK 显示，配置受保护的输出
- OPM WDK 显示，获取受保护的输出信息
- OPM WDK 显示，获取图形适配器信息
- 保护级别 WDK 显示，更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fa6addf3f39323f98fe69ed36ed4c61cc8e7ad4
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185185"
---
# <a name="using-the-opm-ddi"></a>使用 OPM DDI

Microsoft DirectX graphics 内核子系统 (*Dxgkrnl.sys*) 使用 OPM DDI 来创建 OPM 保护的输出、销毁 OPM 受保护的输出、获取证书、配置受保护的输出、获取有关受保护的输出的信息，以及获取有关图形适配器的信息。 当 DirectX 图形内核子系统调用显示微型端口驱动程序的 [**DxgkDdiQueryInterface**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 函数来查询 GUID_DEVINTERFACE_OPM 和 DXGK_OPM_INTERFACE_VERSION_1 标识的接口时，将获取指向 OPM DDI 函数的指针。 下面的序列描述了如何使用 OPM DDI 来创建、操作和销毁 OPM 保护的输出：

1. DirectX 图形内核子系统将调用 [**DxgkDdiOPMCreateProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output) 函数来创建 OPM 保护的输出。 OPM 保护的输出始终只对应于一个物理视频输出。 *DxgkDdiOPMCreateProtectedOutput* 将返回新创建的输出的句柄。

2. DirectX 图形内核子系统调用 [**DxgkDdiOPMGetCertificateSize**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size) 和 [**DxgkDdiOPMGetCertificate**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate) 函数，以获取显示微型端口驱动程序的 OPM 证书或 COPP 证书及其大小。

   > [!NOTE]
   > *DxgkDdiOPMCreateProtectedOutput*、 *DxgkDdiOPMGetCertificateSize*和 *DxgkDdiOPMGetCertificate* 是 DirectX 图形内核子系统不会将受保护的输出句柄传递到的唯一 OPM DDI 函数。

3. DirectX 图形内核子系统将调用 [**DxgkDdiOPMGetRandomNumber**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number) 函数，以获取受保护的输出的随机数字。

4. DirectX 图形内核子系统在对 [**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers) 函数的调用中传递256字节缓冲区。 该缓冲区包含用一个显示微型端口驱动程序的公钥进行加密的数据。 有关公钥的详细信息，请从 [输出内容保护和 Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc) 网站下载内容保护文档的输出。 使用的公钥依赖于受保护的输出的语义。 如果受保护的输出具有 OPM 语义，则使用显示微型端口驱动程序的 OPM 证书中的公钥。 如果受保护的输出具有 COPP 语义，则使用显示微型端口驱动程序的 COPP 证书中的公钥。 用于对数据进行加密的加密方案也依赖于受保护的输出的语义。 如果受保护的输出具有 COPP 语义，且受保护的输出具有 OPM 语义，则数据将通过标准 RSA 算法进行加密。 有关 RSA、AES 和 RSAES-OAEP-ENCRYPT 的信息，请参阅 [Rsa 实验室](https://www.rsa.com/) 网站。 显示微型端口驱动程序使用适当的私钥和解密方法来解密数据。 随机数字、两个随机序列号和128位 AES 密钥位于解密的数据中。 显示微型端口驱动器确保随机数字与驱动程序在调用 [**DxgkDdiOPMGetRandomNumber**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number) 函数时返回的随机数字匹配。 然后，该驱动程序存储两个序列号和128位 AES 密钥。

5. DirectX 图形内核子系统现在可以调用 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information) 或 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) 函数来获取受保护的输出中的信息。 DirectX 图形内核子系统还可以调用 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 配置受保护的输出。 仅当输出具有 OPM 语义并且只有在输出具有 COPP 语义时才能调用*DxgkDdiOPMGetCOPPCompatibleInformation* ，才能调用*DxgkDdiOPMGetInformation* 。 通常，DirectX 图形内核子系统调用 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation* 来获取有关输出的信息，然后调用 *DxgkDdiOPMConfigureProtectedOutput* 一次或多次，以配置输出。 然后，DirectX 图形内核子系统再次调用 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation* 。 DirectX 图形内核子系统可以通过调用 *DxgkDdiOPMGetInformation* 或 *DxgkDdiOPMGetCOPPCompatibleInformation*获取以下类型的信息：

    - 输出的连接器类型。
    - 输出支持的内容保护类型。 输出当前支持：
      - [模拟复制保护 (ACP) ](https://business.tivo.com/services/acp-technology)
      - [内容生成管理系统模拟 (CGMS-A) ](cgms-a-standards.md)
      - [高带宽数字内容保护 (HDCP) ](https://www.digital-cp.com/hdcp-specifications)
      - [DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382) 内容保护 (DPCP) 
    - 特定保护类型的输出的当前虚拟保护级别。
    - 特定保护类型的物理输出的实际保护级别。
    - 该输出当前使用的 HDCP System Renewability 消息 (SRM) 的版本。 有关 HDCP SRM 的详细信息，请参阅 [Hdcp 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。 只有 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information) 可以获取此信息。
    - 连接 HDCP 设备的键选择向量 (KSV) ，以及 HDCP 设备是否为中继器。 只有 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) 可以获取此信息。 有关 HDCP 中继器和 KSVs 的详细信息，请参阅 [Hdcp 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。
    - 图形适配器使用的扩展总线的类型。 PCI 和 AGP 是扩展总线的示例。
    - 从与受保护的输出关联的物理连接器发送到监视器的图像的格式。
    - 受保护的输出支持的 CGMS 和 ACP 信号标准。 只有 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) 可以获取此信息。
    - 输出的标识符。
    - 数字视频接口的电气特征 (DVI) 输出连接器。

    DirectX 图形内核子系统可以通过调用 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)更改以下设置：

    - 输出的某个保护类型的当前保护级别。 例如， *DxgkDdiOPMConfigureProtectedOutput* 可以启用或禁用 HDCP，并可以关闭 ACP 保护或更改当前 ACP 保护级别。
    - 受保护的输出使用的当前 HDCP SRM。
    - 受保护的输出使用的当前信号标准。 仅当输出具有 COPP 语义时才可以进行此更改。

6. DirectX 图形内核子系统在使用受保护的输出对象后调用 [**DxgkDdiOPMDestroyProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output) 。
