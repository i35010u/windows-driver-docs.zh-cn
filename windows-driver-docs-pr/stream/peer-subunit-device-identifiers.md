---
title: 对等子单元设备标识符
description: 对等子单元设备标识符
ms.assetid: f33c554b-77a7-4879-875e-12210b8a553f
keywords:
- AV/C WDK 标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc.sys 功能驱动程序 WDK，标识符
- 对等子单元设备标识符 WDK AV/C
- 子单元支持 WDK AV/C
- 硬件 Id WDK AV/C
- 兼容 Id WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d2e8099058ab6524d79c43aaf285882cd6954c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366501"
---
# <a name="peer-subunit-device-identifiers"></a>对等子单元设备标识符


下面的示例的硬件标识符和兼容的标识符都由*Avc.sys*标准版设备 （即，报告一个或多个子单元连接的设备） 中所述的格式基于[AV/C设备 Id](av-c-device-identifiers.md):

-   生成的硬件标识符*Avc.sys*:

<a href="" id="avc-vendor-model-subunittype-subunitid"></a>**AVC\\*Vendor*&*Model*&*SubunitType*&*SubunitID***  
此硬件标识符是最完整的但因为子单元标识符 （最后一个与符号分隔的部分设备标识符 (ID)） 通常不感兴趣的很少指定 INF 文件中。

<a href="" id="avc-vendor-model-subunittype"></a>**AVC\\*Vendor*&*Model*&*SubunitType***  
尤其是在可以有多个相同的子单元连接时，此样式的设备标识符是 INF 文件中使用的首选***SubunitType***字段在设备上 （这些子单元连接共享相同的子单元驱动程序）。 此格式可由硬件供应商或 microsoft，具体取决于谁提供子单元驱动程序。

-   由生成兼容标识符*Avc.sys*:

<a href="" id="avc-vendor-subunittype"></a>**AVC\\*Vendor*&*SubunitType***  
用于特定于供应商的子单元驱动程序。 通常用于仅在由 Microsoft 提供的 INF 文件中加载由 Microsoft 提供的子单元的子单元连接良好定义的类的驱动程序。

<a href="" id="avc-subunittype"></a>**AVC\\*SubunitType***  
用于 AV/C 子单元特定于驱动程序。 通常用于仅在由 Microsoft 提供的 INF 文件中加载由 Microsoft 提供的子单元的子单元连接良好定义的类的驱动程序。

-   *Avc.sys*不会生成以下兼容标识符：

<a href="" id="avc-subunittype-subunitid"></a>**AVC\\*SubunitType*&*SubunitID***  
执行特定于标识符的任何操作可以完成而无需***供应商***字段。

<a href="" id="avc-vendor"></a>**AVC\\*Vendor***  
特定于供应商的"通用"的子单元驱动程序应包括支持**AVC\\*供应商*&&lt;SubunitType&gt;** 其 INF 文件中的条目而不是使用此格式。

<a href="" id="avc-generic"></a>**AVC\\GENERIC**  
"通用"的子单元驱动程序应包括支持**AVC\\&lt;SubunitType&gt;** 条目中其 INF 文件而不是使用此格式。

下面的示例的硬件标识符和兼容的标识符都由*Avc.sys*摄像机设备 （一个照相机子单元、 一个 VTR 子单元，与任意数量的其他子单元连接的设备）：

-   由生成的硬件标识符*Avc.sys*:

<a href="" id="avc-vendor-model-camcorder"></a>**AVC\\*供应商*&*模型*& 摄像机**  
如果在特定于供应商的 INF 文件中使用*Msdv.sys*将不会加载。

-   由生成兼容标识符*Avc.sys*:

<a href="" id="avc-vendor-camcorder"></a>**AVC\\*供应商*& 摄像机**  
在中使用*Msdv.inf*加载*Msdv.sys*。

<a href="" id="avc-camcorder"></a>**AVC\\CAMCORDER**  
在中使用*Msdv.inf*加载*Msdv.sys*。

-   *Avc.sys*不会生成以下兼容标识符：

<a href="" id="avc-vendor"></a>**AVC\\*Vendor***  
特定于供应商、 通用子单元驱动程序应包括支持**AVC\\*供应商*& CAMCORDER**其 INF 文件中的条目。

<a href="" id="avc-generic"></a>**AVC\\GENERIC**  
通用子单元驱动程序应包括支持**AVC\\CAMCORDER**其 INF 文件中的条目。

**请注意**  :在 Windows Vista、 Windows Server 2003 和 Windows XP 操作系统上，DV 特定于发现机制已添加到*Avc.sys* ，以便任何 DV 磁带设备 （包括摄影机） 将具有"& DV"追加到的硬件标识符和生成的兼容标识符*Avc.sys*。 对于所有 VTR 子单元连接默认情况下启用了此机制 (其中***SubunitType*** = = 4)。 例如，硬件标识符**AVC\\*供应商*&*模型*& CAMCORDER**变得**AVC\\*供应商*&*模型*& 摄像机 & DV**如果子单元是 DV 设备。 可以通过指定将安装在设备 INF 文件中禁用机制**AvcFlags**而无需设置位 3 (**AvcFlags & 0x8** = = 0)。

 

硬件标识符和生成的兼容标识符*Avc.sys*为非标准的和不符合要求的设备才会公开如果**AvcFlags**注册表值具有 1 设置位 (**AvcFlags &** 0x2 = = 0x2)。 必须通过设备 INF 文件设置此标志。 设备的 INF 文件中的以下行 （下面中以粗体显示） 可用于安装硬件时公开了非标准的和不符合要求的设备：

```INF
[CompanyName] ;INF Models section
%Subunit.DeviceDesc%=Subunit,AVC\GENERIC

[Subunit.NT] ;INF DDInstall section
;Other installation directives
AddReg=Subunit.NT.AddReg

[Subunit.NT.AddReg]
;Other registry settings
HKR,,"AvcFlags",0x00000001,0x2 ;0x00000001 = Binary value, 0x2 = Registry key value

[Strings]
;Other strings
Subunit.DeviceDesc="Fabrikam, Inc. Subunit"
```

设备标识符的以下示例生成的*Avc.sys*适用于使用了非标准的和不符合要求的设备时位 1 **AvcFlags**设置：

-   硬件标识符

<a href="" id="avc-vendor-model"></a>**AVC\\*Vendor*&*Model***  
在特定于供应商的 INF 文件中用于加载非标准的和不符合设备的驱动程序。

-   兼容的标识符

<a href="" id="avc-vendor"></a>**AVC\\*Vendor***  
特定于供应商的通用设备驱动程序在其 INF 文件中包括此项。

<a href="" id="avc-generic"></a>**AVC\\GENERIC**  
通用设备驱动程序在其 INF 文件中包括此项。

以下是硬件标识符和兼容的标识符的示例。 请注意，该公司"Fabrikam，Inc." 使用的供应商代码 0x50F2***供应商***字段。

A Fabrikam, Inc.DV 摄像机 （回想一下上面的说明从摄像机是一种特殊情况）：

-   摄像机的硬件标识符：

<a href="" id="avc-ven-50f2-mod-0-camcorder-dv--can-be-used-by-fabrikam--inc--in-an-inf-file-to-override-msdv-sys-as-the-driver-for-their-av-c-device--"></a>**AVC\\即使\_50F2 & MOD\_0 摄像机 & DV** (Fabrikam，Inc.的 INF 文件可用于重写*Msdv.sys*作为其 AV/C 设备的驱动程序)。  

-   摄像机兼容标识符：

<a href="" id="avc-ven-50f2-camcorder-dv--this-is-the-style-of-device-identifier-used-in-msdv-inf-to-load-msdv-sys-"></a>**AVC\\即使\_50F2 & 摄像机 & DV** (这是设备标识符中使用的样式*Msdv.inf*加载*Msdv.sys*)  

<a href="" id="avc-camcorder-dv"></a>**AVC\\CAMCORDER&DV**  

A Fabrikam, Inc.DVHS 磁带一副纸牌调谐器子单元和一个磁带记录器/播放机子单元：

-   磁带记录器/播放机子单元 (其中***SubunitType*** = 4) 的设备标识符会显示在 INF 文件作为：

<a href="" id="avc-ven-50f2-mod-0-typ-4-id-0"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_4&ID\_0**  

-   将磁带记录器/播放机子单元兼容标识符：

<a href="" id="avc-ven-50f2-mod-0-typ-4"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_4**  

<a href="" id="avc-ven-50f2-typ-4--used-in-mstape-inf-to-load-mstape-sys-"></a>**AVC\\即使\_50F2 & TYP\_4** (用于*Mstape.inf*加载*Mstape.sys*)  

<a href="" id="avc-typ-4"></a>**AVC\\TYP\_4**  

-   调谐器子单元 (其中***SubunitType*** = 5) 设备标识符会显示在 INF 文件作为：

<a href="" id="avc-ven-50f2-mod-0-typ-5-id-0"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_5&ID\_0**  

-   将调谐器子单元兼容标识符：

<a href="" id="avc-ven-50f2-mod-0-typ-5"></a>**AVC\\VEN\_50F2&MOD\_0&TYP\_5**  

<a href="" id="avc-ven-50f2-typ-5"></a>**AVC\\VEN\_50F2&TYP\_5**  

<a href="" id="avc-typ-5"></a>**AVC\\TYP\_5**  

**请注意**  :供应商应仅在上述情况下指定的硬件标识符并永远不会指定兼容的标识符。 此外，供应商应提供任何由 Microsoft 提供的 INF 文件中找到相匹配的设备标识符。

 

 

 




