---
title: 检索 OPM DDI
description: 检索 OPM DDI
ms.assetid: 84218245-f5f3-4a6f-88ed-9cd5db224e30
keywords:
- OPM WDK 显示，检索 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31b3f6765429a5bd2db929aa3aef01e9b4e783dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825837"
---
# <a name="retrieving-the-opm-ddi"></a>检索 OPM DDI


以下序列显示了 Microsoft DirectX graphics 内核子系统（Dxgkrnl）如何检索显示微型端口驱动程序的[OPM DDI](supporting-output-protection-manager.md)：

1. DirectX 图形内核子系统调用显示微型端口驱动程序的[**DxgkDdiAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)函数，以创建图形适配器的上下文块并返回该图形适配器的句柄。

2. DirectX 图形内核子系统使用下表中的值初始化[**查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)结构。

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
   <th align="left">Value</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceType</strong></p></td>
   <td align="left"><p>CONST PGUID</p></td>
   <td align="left"><p>指向 GUID_DEVINTERFACE_OPM 的指针</p>
   <p>(BF4672DE-6B4E-4BE4-A325-68A91EA49C09)</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>大小</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>sizeof （DXGK_OPM_INTERFACE）</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>版本</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>DXGK_OPM_INTERFACE_VERSION_1</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>Interface</strong></p></td>
   <td align="left"><p>PINTERFACE</p></td>
   <td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface" data-raw-source="[&lt;strong&gt;DXGK_OPM_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)"><strong>DXGK_OPM_INTERFACE</strong></a>结构的指针</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceSpecificData</strong></p></td>
   <td align="left"><p>PVOID</p></td>
   <td align="left"><p>NULL</p></td>
   </tr>
   </tbody>
   </table>

     

3. 在对显示微型端口驱动程序的[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数的调用中，DirectX 图形内核子系统将初始化的查询传递\_接口。

4. 如果显示微型端口驱动程序不支持 OPM 接口，则[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)必须返回状态\_不\_支持。

   如果显示微型端口驱动程序支持 OPM，则[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)会将在[ **\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)的**接口**成员中收到的[**DXGK\_OPM\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)结构替换为值在下表中。

   **成员名称、类型和值：**

   <span id="Size"></span><span id="size"></span><span id="SIZE"></span>**规格**  
   类型 USHORT

   sizeof （DXGK\_OPM\_INTERFACE）

   <span id="Version"></span><span id="version"></span><span id="VERSION"></span>**版本**  
   类型 USHORT

   DXGK\_OPM\_INTERFACE\_版本\_1

   <span id="InterfaceReference"></span><span id="interfacereference"></span><span id="INTERFACEREFERENCE"></span>**InterfaceReference**  
   键入 PINTERFACE\_引用

   一个指针，指向显示微型端口驱动程序的**InterfaceReference**例程（有关**InterfaceReference**的详细信息，请参阅[**接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)结构的 "备注" 部分。）

   <span id="InterfaceDereference"></span><span id="interfacedereference"></span><span id="INTERFACEDEREFERENCE"></span>**InterfaceDereference**  
   键入 PINTERFACE\_取消引用

   一个指针，指向显示微型端口驱动程序的**InterfaceDereference**例程（有关**InterfaceDereference**的详细信息，请参阅[**接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)结构的 "备注" 部分。）

   <span id="DxgkDdiOPMGetCertificateSize"></span><span id="dxgkddiopmgetcertificatesize"></span><span id="DXGKDDIOPMGETCERTIFICATESIZE"></span>**DxgkDdiOPMGetCertificateSize**  
   键入 DXGKDDI\_OPM\_获取\_证书\_大小

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMGetCertificateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)函数

   <span id="DxgkDdiOPMGetCertificate"></span><span id="dxgkddiopmgetcertificate"></span><span id="DXGKDDIOPMGETCERTIFICATE"></span>**DxgkDdiOPMGetCertificate**  
   键入 DXGKDDI\_OPM\_获取\_证书

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMGetCertificate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)函数

   <span id="DxgkDdiOPMCreateProtectedOutput"></span><span id="dxgkddiopmcreateprotectedoutput"></span><span id="DXGKDDIOPMCREATEPROTECTEDOUTPUT"></span>**DxgkDdiOPMCreateProtectedOutput**  
   键入 DXGKDDI\_OPM\_创建\_保护\_输出

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)函数

   <span id="DxgkDdiOPMGetRandomNumber"></span><span id="dxgkddiopmgetrandomnumber"></span><span id="DXGKDDIOPMGETRANDOMNUMBER"></span>**DxgkDdiOPMGetRandomNumber**  
   键入 DXGKDDI\_OPM\_获取\_随机\_号

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMGetRandomNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)函数

   <span id="DxgkDdiOPMSetSigningKeyAndSequenceNumbers"></span><span id="dxgkddiopmsetsigningkeyandsequencenumbers"></span><span id="DXGKDDIOPMSETSIGNINGKEYANDSEQUENCENUMBERS"></span>**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**  
   DXGKDDI\_OPM\_设置\_签名\_密钥\_和\_序列\_号

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)函数

   <span id="DxgkDdiOPMGetInformation"></span><span id="dxgkddiopmgetinformation"></span><span id="DXGKDDIOPMGETINFORMATION"></span>**DxgkDdiOPMGetInformation**  
   DXGKDDI\_OPM\_获取\_信息

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)函数

   <span id="DxgkDdiOPMGetCOPPCompatibleInformation"></span><span id="dxgkddiopmgetcoppcompatibleinformation"></span><span id="DXGKDDIOPMGETCOPPCOMPATIBLEINFORMATION"></span>**DxgkDdiOPMGetCOPPCompatibleInformation**  
   DXGKDDI\_OPM\_获取\_COPP\_兼容的\_信息

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)函数

   <span id="DxgkDdiOPMConfigureProtectedOutput"></span><span id="dxgkddiopmconfigureprotectedoutput"></span><span id="DXGKDDIOPMCONFIGUREPROTECTEDOUTPUT"></span>**DxgkDdiOPMConfigureProtectedOutput**  
   DXGKDDI\_OPM\_配置\_保护的\_输出

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数

   <span id="DxgkDdiOPMDestroyProtectedOutput"></span><span id="dxgkddiopmdestroyprotectedoutput"></span><span id="DXGKDDIOPMDESTROYPROTECTEDOUTPUT"></span>**DxgkDdiOPMDestroyProtectedOutput**  
   DXGKDDI\_OPM\_销毁\_保护的\_输出

   一个指针，指向显示微型端口驱动程序的[**DxgkDdiOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)函数

5. 当使用 OPM 接口完成显示微型端口驱动程序时，驱动程序将调用其**InterfaceDereference**例程。 在调用[**DxgkDdiRemoveDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)函数之前，驱动程序应调用**InterfaceDereference** 。

 

 





