---
title: 使用 OPM DDI
description: 使用 OPM DDI
ms.assetid: cd3c78a4-0241-48ab-9005-c544db199eb5
keywords:
- 有关 DDI OPM WDK 显示器
- 创建受保护的 OPM WDK 显示器输出
- 销毁受保护的 OPM WDK 显示器输出
- OPM WDK 显示，获得证书
- OPM WDK 显示中，配置受保护的输出
- OPM WDK 显示，获取受保护的输出信息
- OPM WDK 显示，获取图形适配器信息
- 保护级别 WDK 显示更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075b9140c82d314dd60f18ed99e0b56809b304f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388976"
---
# <a name="using-the-opm-ddi"></a>使用 OPM DDI


Microsoft DirectX 图形内核子系统 (*Dxgkrnl.sys*) 使用 OPM DDI 创建 OPM 受保护的输出、 销毁 OPM 受保护的输出，获取证书、 配置受保护的输出，获取信息大约保护输出和获取有关图形适配器的信息。 DirectX 图形内核子系统获取 OPM DDI 函数指针调用显示微型端口驱动程序时[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)用于标识接口查询函数按 GUID\_DEVINTERFACE\_OPM 和 DXGK\_OPM\_接口\_版本\_1。 以下序列描述了如何 OPM DDI 通常用于创建、 操作和销毁 OPM 受保护的输出：

1.  DirectX 图形内核子系统调用[ **DxgkDdiOPMCreateProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559705)函数来创建 OPM 受保护的输出。 受保护的 OPM 输出始终对应于一个物理的视频输出。 *DxgkDdiOPMCreateProtectedOutput*返回的句柄的新创建的输出。

2.  DirectX 图形内核子系统调用[ **DxgkDdiOPMGetCertificateSize** ](https://msdn.microsoft.com/library/windows/hardware/ff559715)并[ **DxgkDdiOPMGetCertificate** ](https://msdn.microsoft.com/library/windows/hardware/ff559711)若要获取显示微型端口驱动程序的 OPM 证书或 COPP 证书和其大小的函数。
    **请注意**  *DxgkDdiOPMCreateProtectedOutput*， *DxgkDdiOPMGetCertificateSize*，并且*DxgkDdiOPMGetCertificate*是唯一的 OPM DDI 函数DirectX 图形内核子系统未通过的受保护的输出句柄。

     

3.  DirectX 图形内核子系统调用[ **DxgkDdiOPMGetRandomNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff559730)函数以获取受保护的输出的随机数字。

4.  DirectX 图形内核子系统将对的调用中传递的 256 字节缓冲区[ **DxgkDdiOPMSetSigningKeyAndSequenceNumbers** ](https://msdn.microsoft.com/library/windows/hardware/ff559735)函数。 在缓冲区中包含使用其中一个显示微型端口驱动程序的公共密钥加密的数据。 有关公共密钥的详细信息，请下载中的输出内容保护文档[输出内容保护和 Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)网站。 使用的公钥取决于受保护的输出的语义。 如果受保护的输出不含 OPM 语义，使用显示微型端口驱动程序的 OPM 证书中的公钥。 如果受保护的输出不含 COPP 语义，使用显示微型端口驱动程序的 COPP 证书中的公钥。 用于加密数据的加密方案还取决于受保护的输出的语义。 对数据进行加密与标准的 RSA 算法，如果受保护的输出不含 COPP 语义和 RSAES OAEP 加密方案，如果受保护的输出不含 OPM 语义。 RSA 和 AES，RSAES OAEP 有关的信息，请参阅[RSA Laboratories](https://go.microsoft.com/fwlink/p/?linkid=70411)网站。 显示微型端口驱动程序使用适当的专用密钥和解密方法对数据进行解密。 中已解密的数据的随机数字，两个随机序列号和一个 128 位 AES 密钥。 显示微型端口驱动器可以确保随机数字与随机数字时，返回该驱动程序匹配其[ **DxgkDdiOPMGetRandomNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff559730)调用函数。 两个序列号和 128 位 AES 密钥，然后将存储驱动程序。

5.  现在可以调用 DirectX 图形内核子系统[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)或[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)函数来从受保护的输出中获取信息。 此外可以调用 DirectX 图形内核子系统[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)若要配置受保护的输出。 *DxgkDdiOPMGetInformation*输出具有 OPM 语义的情况下，才可以调用并*DxgkDdiOPMGetCOPPCompatibleInformation*输出具有 COPP 语义的情况下，才可以调用。 通常情况下，DirectX 图形内核子系统调用*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*若要获取有关输出，然后调用信息*DxgkDdiOPMConfigureProtectedOutput*若要配置输出的一个或多个时间。 然后，调用 DirectX 图形内核子系统*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*试。 DirectX 图形内核子系统可以获取以下类型的信息，通过调用*DxgkDdiOPMGetInformation*或*DxgkDdiOPMGetCOPPCompatibleInformation*:

    -   连接器的输出的类型。
    -   输出支持的内容保护的类型。 输出当前支持模拟复制保护 (ACP)[内容生成管理系统模拟 (CGMS A)](cgms-a-standards.md)，高带宽数字内容保护 (HDCP) 和内容保护 DisplayPort (DPCP)。 有关 ACP 详细信息，请参阅[Rovi (以前称为 Macrovision)](https://go.microsoft.com/fwlink/p/?linkid=71273)网站。 有关 HDCP 详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。 有关 DisplayPort 详细信息，请参阅[DisplayPort](https://go.microsoft.com/fwlink/p/?linkid=71382) Web 项目。
    -   输出的当前虚拟保护级别为特定的保护类型的。
    -   特定的保护类型的物理输出实际的保护级别。
    -   版本的输出当前使用 HDCP 系统可更新性消息 (SRM)。 有关 HDCP SRM 详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。 仅[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)可以获取此信息。
    -   已连接的 HDCP 设备密钥选择矢量 (KSV) 和 HDCP 设备是 repeater。 仅[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)可以获取此信息。 有关 HDCP 重复字符和 KSVs 的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。
    -   图形适配器使用的扩展总线类型。 PCI 和 AGP 是扩展总线的示例。
    -   从与受保护的输出与监视器关联的物理连接器发送的图像的格式。
    -   CGMS A 和 ACP 信号标准，支持受保护的输出。 仅[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)可以获取此信息。
    -   输出的标识符。
    -   电力特征的数字视频接口 (DVI) 输出连接器。

    DirectX 图形内核子系统可以更改以下设置，通过调用[ **DxgkDdiOPMConfigureProtectedOutput**](https://msdn.microsoft.com/library/windows/hardware/ff559701):

    -   当前的输出的保护类型之一的保护级别。 例如， *DxgkDdiOPMConfigureProtectedOutput*可以启用或禁用 HDCP 和可以关闭 ACP 保护或更改当前的 ACP 保护级别。
    -   受保护的输出会使用当前 HDCP SRM。
    -   受保护的输出会使用当前信号标准。 仅当输出包含 COPP 语义可进行此更改。

6.  DirectX 图形内核子系统调用[ **DxgkDdiOPMDestroyProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559708)完成使用受保护的输出对象后。

 

 





