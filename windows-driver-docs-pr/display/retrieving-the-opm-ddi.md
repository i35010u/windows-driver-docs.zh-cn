---
title: 检索 OPM DDI
description: 检索 OPM DDI
ms.assetid: 84218245-f5f3-4a6f-88ed-9cd5db224e30
keywords:
- OPM WDK 显示，检索 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b178d08fc6616c6b81d860a97e8587f0bf600347
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525716"
---
# <a name="retrieving-the-opm-ddi"></a>检索 OPM DDI


按以下顺序显示了如何在 Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 检索显示微型端口驱动程序[OPM DDI](supporting-output-protection-manager.md):

1. DirectX 图形内核子系统调用显示微型端口驱动程序[ **DxgkDdiAddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559586)函数创建图形适配器的上下文块并对该图形适配器返回的句柄。

2. DirectX 图形内核子系统初始化[**查询\_界面**](https://msdn.microsoft.com/library/windows/hardware/ff569225)结构具有下表中的值。

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
   <td align="left"><p>指向 GUID_DEVINTERFACE_OPM</p>
   <p>(BF4672DE-6B4E-4BE4-A325-68A91EA49C09)</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>大小</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>sizeof(DXGK_OPM_INTERFACE)</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>版本</strong></p></td>
   <td align="left"><p>USHORT</p></td>
   <td align="left"><p>DXGK_OPM_INTERFACE_VERSION_1</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>接口</strong></p></td>
   <td align="left"><p>PINTERFACE</p></td>
   <td align="left"><p>一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff561986" data-raw-source="[&lt;strong&gt;DXGK_OPM_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561986)"> <strong>DXGK_OPM_INTERFACE</strong> </a>结构</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><p><strong>InterfaceSpecificData</strong></p></td>
   <td align="left"><p>PVOID</p></td>
   <td align="left"><p>NULL</p></td>
   </tr>
   </tbody>
   </table>

     

3. DirectX 图形内核子系统将初始化的查询传递\_界面中显示微型端口驱动程序的调用[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)函数。

4. 如果显示微型端口驱动程序不支持 OPM 接口[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)必须返回状态\_不\_受支持。

   如果显示微型端口驱动程序支持 OPM， [ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)初始化[ **DXGK\_OPM\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff561986)中收到的结构**接口**的成员[**查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff569225)中的值下表。

   **成员名称、 类型和值：**

   <span id="Size"></span><span id="size"></span><span id="SIZE"></span>**大小**  
   类型 USHORT

   sizeof(DXGK\_OPM\_INTERFACE)

   <span id="Version"></span><span id="version"></span><span id="VERSION"></span>**版本**  
   类型 USHORT

   DXGK\_OPM\_INTERFACE\_VERSION\_1

   <span id="InterfaceReference"></span><span id="interfacereference"></span><span id="INTERFACEREFERENCE"></span>**InterfaceReference**  
   键入 PINTERFACE\_引用

   显示微型端口驱动程序的一个指向**InterfaceReference**例程 (有关信息**InterfaceReference**，请参阅备注部分的[**接口** ](https://msdn.microsoft.com/library/windows/hardware/ff547825)结构。)

   <span id="InterfaceDereference"></span><span id="interfacedereference"></span><span id="INTERFACEDEREFERENCE"></span>**InterfaceDereference**  
   键入 PINTERFACE\_取消引用

   显示微型端口驱动程序的一个指向**InterfaceDereference**例程 (有关信息**InterfaceDereference**，请参阅备注部分的[**接口** ](https://msdn.microsoft.com/library/windows/hardware/ff547825)结构。)

   <span id="DxgkDdiOPMGetCertificateSize"></span><span id="dxgkddiopmgetcertificatesize"></span><span id="DXGKDDIOPMGETCERTIFICATESIZE"></span>**DxgkDdiOPMGetCertificateSize**  
   Type DXGKDDI\_OPM\_GET\_CERTIFICATE\_SIZE

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMGetCertificateSize** ](https://msdn.microsoft.com/library/windows/hardware/ff559715)函数

   <span id="DxgkDdiOPMGetCertificate"></span><span id="dxgkddiopmgetcertificate"></span><span id="DXGKDDIOPMGETCERTIFICATE"></span>**DxgkDdiOPMGetCertificate**  
   Type DXGKDDI\_OPM\_GET\_CERTIFICATE

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMGetCertificate** ](https://msdn.microsoft.com/library/windows/hardware/ff559711)函数

   <span id="DxgkDdiOPMCreateProtectedOutput"></span><span id="dxgkddiopmcreateprotectedoutput"></span><span id="DXGKDDIOPMCREATEPROTECTEDOUTPUT"></span>**DxgkDdiOPMCreateProtectedOutput**  
   键入 DXGKDDI\_OPM\_创建\_受保护\_输出

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMCreateProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559705)函数

   <span id="DxgkDdiOPMGetRandomNumber"></span><span id="dxgkddiopmgetrandomnumber"></span><span id="DXGKDDIOPMGETRANDOMNUMBER"></span>**DxgkDdiOPMGetRandomNumber**  
   键入 DXGKDDI\_OPM\_获取\_随机\_数

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMGetRandomNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff559730)函数

   <span id="DxgkDdiOPMSetSigningKeyAndSequenceNumbers"></span><span id="dxgkddiopmsetsigningkeyandsequencenumbers"></span><span id="DXGKDDIOPMSETSIGNINGKEYANDSEQUENCENUMBERS"></span>**DxgkDdiOPMSetSigningKeyAndSequenceNumbers**  
   DXGKDDI\_OPM\_设置\_签名\_密钥\_AND\_序列\_数字

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMSetSigningKeyAndSequenceNumbers** ](https://msdn.microsoft.com/library/windows/hardware/ff559735)函数

   <span id="DxgkDdiOPMGetInformation"></span><span id="dxgkddiopmgetinformation"></span><span id="DXGKDDIOPMGETINFORMATION"></span>**DxgkDdiOPMGetInformation**  
   DXGKDDI\_OPM\_GET\_INFORMATION

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)函数

   <span id="DxgkDdiOPMGetCOPPCompatibleInformation"></span><span id="dxgkddiopmgetcoppcompatibleinformation"></span><span id="DXGKDDIOPMGETCOPPCOMPATIBLEINFORMATION"></span>**DxgkDdiOPMGetCOPPCompatibleInformation**  
   DXGKDDI\_OPM\_GET\_COPP\_COMPATIBLE\_INFORMATION

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)函数

   <span id="DxgkDdiOPMConfigureProtectedOutput"></span><span id="dxgkddiopmconfigureprotectedoutput"></span><span id="DXGKDDIOPMCONFIGUREPROTECTEDOUTPUT"></span>**DxgkDdiOPMConfigureProtectedOutput**  
   DXGKDDI\_OPM\_配置\_受保护\_输出

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)函数

   <span id="DxgkDdiOPMDestroyProtectedOutput"></span><span id="dxgkddiopmdestroyprotectedoutput"></span><span id="DXGKDDIOPMDESTROYPROTECTEDOUTPUT"></span>**DxgkDdiOPMDestroyProtectedOutput**  
   DXGKDDI\_OPM\_DESTROY\_PROTECTED\_OUTPUT

   显示微型端口驱动程序的一个指向[ **DxgkDdiOPMDestroyProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559708)函数

5. 显示微型端口驱动程序完成后使用 OPM 接口，驱动程序调用其**InterfaceDereference**例程。 该驱动程序应调用**InterfaceDereference**之前其[ **DxgkDdiRemoveDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff559789)调用函数。

 

 





