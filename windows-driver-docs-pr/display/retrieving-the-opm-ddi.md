---
title: 检索 OPM DDI
description: 检索 OPM DDI
ms.assetid: 84218245-f5f3-4a6f-88ed-9cd5db224e30
keywords:
- OPM WDK 显示，检索 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e12c67dc55458d405b6edf03ff79af182bc99d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106614"
---
# <a name="retrieving-the-opm-ddi"></a>检索 OPM DDI


以下序列显示了 Microsoft DirectX graphics 内核子系统 ( # A0) 如何检索显示微型端口驱动程序的 [OPM DDI](supporting-output-protection-manager.md)：

1. DirectX 图形内核子系统调用显示微型端口驱动程序的 [**DxgkDdiAddDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device) 函数，以创建图形适配器的上下文块并返回该图形适配器的句柄。

2. DirectX 图形内核子系统使用下表中的值初始化 [**查询 \_ 接口**](/windows-hardware/drivers/ddi/video/ns-video-_query_interface) 结构。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">成员名称</th>
   <th align="left">成员类型</th>
   <th align="left">值</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceType</strong></p></td>
   <td align="left"><p>CONST PGUID</p></td>
   <td align="left"><p>指向 GUID_DEVINTERFACE_OPM 的指针</p>
   <p> (BF4672DE-6B4E-4BE4-A325-68A91EA49C09) </p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>大小</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>sizeof (DXGK_OPM_INTERFACE) </p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>Version</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>DXGK_OPM_INTERFACE_VERSION_1</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>Interface</strong></p></td>
   <td align="left"><p>PINTERFACE</p></td>
   <td align="left"><p>指向 <a href="/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface" data-raw-source="[&lt;strong&gt;DXGK_OPM_INTERFACE&lt;/strong&gt;](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)"><strong>DXGK_OPM_INTERFACE</strong></a> 结构的指针</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceSpecificData</strong></p></td>
   <td align="left"><p>PVOID</p></td>
   <td align="left"><p>Null</p></td>
   </tr>
   </tbody>
   </table>

     

3. DirectX 图形内核子系统 \_ 在调用显示微型端口驱动程序的 [**DxgkDdiQueryInterface**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 函数时传递已初始化的查询接口。

4. 如果显示微型端口驱动程序不支持 OPM 接口，则 [**DxgkDdiQueryInterface**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 必须返回 \_ 不 \_ 受支持的状态。

   如果显示微型端口驱动程序支持 OPM，则[**DxgkDdiQueryInterface**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)会将在[**查询 \_ 接口**](/windows-hardware/drivers/ddi/video/ns-video-_query_interface)的**接口**成员中收到的[**DXGK \_ OPM \_ 接口**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)结构与下表中的值初始化。

   **成员名称、类型和值：**

   <span id="Size"></span><span id="size"></span><span id="SIZE"></span>**规格**  
   类型 USHORT

   sizeof (DXGK \_ OPM \_ INTERFACE) 

   <span id="Version"></span><span id="version"></span><span id="VERSION"></span>**版本**  
   类型 USHORT

   DXGK \_ OPM \_ 接口 \_ 版本 \_ 1

   <span id="InterfaceReference"></span><span id="interfacereference"></span><span id="INTERFACEREFERENCE"></span>**InterfaceReference**  
   键入 PINTERFACE \_ 引用

   指向显示微型端口驱动程序的 **InterfaceReference** 例程的指针 (有关 **InterfaceReference**的信息，请参阅 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构的 "备注" 部分。 ) 

   <span id="InterfaceDereference"></span><span id="interfacedereference"></span><span id="INTERFACEDEREFERENCE"></span>**InterfaceDereference**  
   键入 PINTERFACE \_ 取消引用

   指向显示微型端口驱动程序的 **InterfaceDereference** 例程的指针 (有关 **InterfaceDereference**的信息，请参阅 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构的 "备注" 部分。 ) 

   <span id="DxgkDdiOPMGetCertificateSize"></span><span id="dxgkddiopmgetcertificatesize"></span><span id="DXGKDDIOPMGETCERTIFICATESIZE"></span>**DxgkDdiOPMGetCertificateSize**  
   键入 DXGKDDI \_ OPM \_ 获取 \_ 证书 \_ 大小

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMGetCertificateSize**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size) 函数

   <span id="DxgkDdiOPMGetCertificate"></span><span id="dxgkddiopmgetcertificate"></span><span id="DXGKDDIOPMGETCERTIFICATE"></span>**DxgkDdiOPMGetCertificate**  
   键入 DXGKDDI \_ OPM \_ 获取 \_ 证书

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMGetCertificate**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate) 函数

   <span id="DxgkDdiOPMCreateProtectedOutput"></span><span id="dxgkddiopmcreateprotectedoutput"></span><span id="DXGKDDIOPMCREATEPROTECTEDOUTPUT"></span>**DxgkDdiOPMCreateProtectedOutput**  
   键入 DXGKDDI \_ OPM \_ 创建 \_ 受保护的 \_ 输出

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMCreateProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output) 函数

   <span id="DxgkDdiOPMGetRandomNumber"></span><span id="dxgkddiopmgetrandomnumber"></span><span id="DXGKDDIOPMGETRANDOMNUMBER"></span>**DxgkDdiOPMGetRandomNumber**  
   键入 DXGKDDI \_ OPM \_ 获取 \_ 随机数 \_

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMGetRandomNumber**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number) 函数

   <span id="DxgkDdiOPMSetSigningKeyAndSequenceNumbers"></span><span id="dxgkddiopmsetsigningkeyandsequencenumbers"></span><span id="DXGKDDIOPMSETSIGNINGKEYANDSEQUENCENUMBERS"></span>**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**  
   DXGKDDI \_ OPM \_ 设置 \_ 签名 \_ 密钥 \_ 和 \_ 序列 \_ 号

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers) 函数

   <span id="DxgkDdiOPMGetInformation"></span><span id="dxgkddiopmgetinformation"></span><span id="DXGKDDIOPMGETINFORMATION"></span>**DxgkDdiOPMGetInformation**  
   DXGKDDI \_ OPM \_ 获取 \_ 信息

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMGetInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information) 函数

   <span id="DxgkDdiOPMGetCOPPCompatibleInformation"></span><span id="dxgkddiopmgetcoppcompatibleinformation"></span><span id="DXGKDDIOPMGETCOPPCOMPATIBLEINFORMATION"></span>**DxgkDdiOPMGetCOPPCompatibleInformation**  
   DXGKDDI \_ OPM \_ 获取 \_ COPP \_ 兼容 \_ 信息

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMGetCOPPCompatibleInformation**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) 函数

   <span id="DxgkDdiOPMConfigureProtectedOutput"></span><span id="dxgkddiopmconfigureprotectedoutput"></span><span id="DXGKDDIOPMCONFIGUREPROTECTEDOUTPUT"></span>**DxgkDdiOPMConfigureProtectedOutput**  
   DXGKDDI \_ OPM \_ 配置 \_ 受保护的 \_ 输出

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMConfigureProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output) 函数

   <span id="DxgkDdiOPMDestroyProtectedOutput"></span><span id="dxgkddiopmdestroyprotectedoutput"></span><span id="DXGKDDIOPMDESTROYPROTECTEDOUTPUT"></span>**DxgkDdiOPMDestroyProtectedOutput**  
   DXGKDDI \_ OPM \_ 销毁 \_ 受保护的 \_ 输出

   一个指针，指向显示微型端口驱动程序的 [**DxgkDdiOPMDestroyProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output) 函数

5. 当使用 OPM 接口完成显示微型端口驱动程序时，驱动程序将调用其 **InterfaceDereference** 例程。 在调用[**DxgkDdiRemoveDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)函数之前，驱动程序应调用**InterfaceDereference** 。

