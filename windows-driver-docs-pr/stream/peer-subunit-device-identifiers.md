---
title: 对等子单元设备标识符
description: 对等子单元设备标识符
keywords:
- AV/C WDK，标识符
- 标识符 WDK AV/C
- 设备 Id WDK AV/C
- Avc.sys 函数驱动程序 WDK，标识符
- 对等子设备标识符 WDK AV/C
- 子次级支持 WDK AV/C
- 硬件 Id WDK AV/C
- 兼容 Id WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9c4b6c1530216cfef2b86450d563daf74bf8488
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840513"
---
# <a name="peer-subunit-device-identifiers"></a>对等子单元设备标识符


以下硬件标识符和兼容标识符的示例由标准设备 *Avc.sys* 生成 (即，基于 [AV/C 设备 id](av-c-device-identifiers.md)中所述的格式报告一个或多个子单元连接) 的设备：

-   *Avc.sys* 生成的硬件标识符：

<a href="" id="avc-vendor-model-subunittype-subunitid"></a>**AVC \\ *供应商* & *型号* & *SubunitType*& * SubunitID***  
此硬件标识符是最完整的，但很少在 INF 文件中指定，因为次级标识符 (设备标识符 () ID 的最后一个符号分隔部分，而不是通常感兴趣。

<a href="" id="avc-vendor-model-subunittype"></a>**AVC \\ *供应商* & *型号*& * SubunitType***  
此样式设备标识符首个用于 INF 文件中，特别是当设备 (上可以有多个子单元连接时 *_SubunitType_*，这些子单元连接共享相同的子) 子驱动程序。 此格式可供硬件供应商或 Microsoft 使用，具体取决于谁提供了次级设备驱动程序。

-   _Avc.sys 生成的兼容标识符：

<a href="" id="avc-vendor-subunittype"></a>**AVC \\ *供应商*& * SubunitType***  
用于供应商特定的子单位驱动程序。 通常仅在 Microsoft 提供的 INF 文件中使用，以便为定义良好的子单元连接类加载 Microsoft 提供的次级设备驱动程序。

<a href="" id="avc-subunittype"></a>**AVC \\ * SubunitType***  
用于 AV/C 子单位特定驱动程序。 通常仅在 Microsoft 提供的 INF 文件中使用，以便为定义良好的子单元连接类加载 Microsoft 提供的次级设备驱动程序。

-   *Avc.sys* 不会生成以下兼容标识符：

<a href="" id="avc-subunittype-subunitid"></a>**AVC \\ *SubunitType*& * SubunitID***  
无需 **_供应商_* _ 字段即可实现标识符特定的任何内容。

<a href="" id="avc-vendor"></a>_ *AVC \\* 供应商 * * *  
特定于供应商的 "通用" 子单位驱动程序应在其 INF 文件中包含受支持的 **AVC \\ *供应商* & &lt; SubunitType &gt;** 条目，而不是使用此格式。

<a href="" id="avc-generic"></a>**AVC \\ 泛型**  
"通用" 子单元驱动程序应在其 INF 文件中包含受支持的 **AVC \\ &lt; &gt; SubunitType** 项，而不是使用此格式。

以下硬件标识符和兼容标识符的示例是 *Avc.sys* 通过以下方法生成的： (设备上带有一个相机子单位的设备、一个 VTR 子单位和任意数量的其他子单元连接) ：

-   *Avc.sys* 生成的硬件标识符：

<a href="" id="avc-vendor-model-camcorder"></a>**&摄像机的 AVC \\ *供应商* & *型号***  
如果不加载 *Msdv.sys* ，则用于特定于供应商的 INF 文件。

-   *Avc.sys* 生成的兼容标识符：

<a href="" id="avc-vendor-camcorder"></a>**AVC \\ *供应商*&摄像机**  
在 *Msdv* 中用于加载 *Msdv.sys*。

<a href="" id="avc-camcorder"></a>**AVC \\ 摄像机**  
在 *Msdv* 中用于加载 *Msdv.sys*。

-   *Avc.sys* 不会生成以下兼容标识符：

<a href="" id="avc-vendor"></a>**AVC \\ * 供应商***  
特定于供应商的通用子单位驱动程序应在其 INF 文件中包含受支持的 **AVC \\ *供应商*&摄像机** 项。

<a href="" id="avc-generic"></a>**AVC \\ 泛型**  
通用子单位驱动程序应在其 INF 文件中包含受支持的 **AVC \\ 摄像机** 项。

**注意**  ：在 windows Vista、windows Server 2003 和 windows XP 操作系统上，已将特定于 dv 的发现机制添加到 *Avc.sys* ，以便任何 dv 磁带设备 (包括摄像机) 会将 "&DV" 追加到 *Avc.sys* 生成的硬件标识符和兼容标识符上。 默认情况下，对所有 VTR 子单元连接 (（其中 ***SubunitType** _ = = 4) 启用此机制。例如，如果次级设备是 dv 设备，则硬件标识符 _ *AVC \\* 供应商 *&* 型号 *&摄像机** 将变为 **AVC \\ *供应商* & *型号*&摄像机&DV** 。可以在 INF 文件中禁用该机制，该文件通过指定 **AvcFlags** ，而不是使用第三个 set ( * * AvcFlags & 0x8** = = 0) 来安装设备。

 

仅当 **AvcFlags** 注册表值具有 bit 1 集 (**AvcFlags &** 0x2 = = 0x2) 时，才会公开为非标准和不相容设备 *Avc.sys* 生成的硬件标识符和兼容标识符。 必须通过设备的 INF 文件设置此标志。 设备 INF 文件中的以下行 (下面的粗体) ，可用于在安装硬件时公开非标准和不相容的设备：

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

设置 **AvcFlags** 的第1位时，为非标准和不相容设备 *Avc.sys* 生成了以下设备标识符示例：

-   硬件标识符

<a href="" id="avc-vendor-model"></a>**AVC \\ *供应商*& * 型号***  
用于为非标准和不符合要求的设备加载驱动程序。

-   兼容标识符

<a href="" id="avc-vendor"></a>**AVC \\ * 供应商***  
特定于供应商的通用单元驱动程序在其 INF 文件中包含此项。

<a href="" id="avc-generic"></a>**AVC \\ 泛型**  
通用单元驱动程序在其 INF 文件中包含此项。

下面是硬件标识符和兼容标识符的示例。 请注意，公司 "Fabrikam，Inc." 对于 **_供应商_* _ 字段，使用供应商代码0x50F2。

Fabrikam，Inc. DV 摄像机 (回忆一下，这是一个特殊情况) 的摄像机：

-   摄像机硬件标识符：

<a href="" id="avc-ven-50f2-mod-0-camcorder-dv--can-be-used-by-fabrikam--inc--in-an-inf-file-to-override-msdv-sys-as-the-driver-for-their-av-c-device--"></a>_ *AVC \\ 即使 \_ 50F2&MOD \_ 0&摄像机&DV** (可由 Fabrikam，inc. 在 INF 文件中使用，以将 *Msdv.sys* 替代为其 AV/C 设备) 的驱动程序。  

-   便携式摄像机兼容标识符：

<a href="" id="avc-ven-50f2-camcorder-dv--this-is-the-style-of-device-identifier-used-in-msdv-inf-to-load-msdv-sys-"></a>**AVC \\即使 \_ 50F2&摄像机&DV** (这是 *Msdv* 中用于加载 *Msdv.sys* 的设备标识符的样式)   

<a href="" id="avc-camcorder-dv"></a>**AVC \\ 摄像机&DV**  

具有一个调谐器子组和一个磁带记录器/播放器子单位的 Fabrikam，Inc. DVHS 磁带卡座：

-   磁带记录器/播放机的子单位 (其中，**_SubunitType_* _ = 4) 设备标识符将显示在 INF 文件中，如下所示：

<a href="" id="avc-ven-50f2-mod-0-typ-4-id-0"></a>_ *AVC \\ 即使 \_ 50F2&MOD \_ 0&TYP \_ 4&ID \_ 0**  

-   磁带记录器/播放器子单位的兼容标识符将为：

<a href="" id="avc-ven-50f2-mod-0-typ-4"></a>**AVC \\ 即使 \_ 50F2&MOD \_ 0&TYP \_ 4**  

<a href="" id="avc-ven-50f2-typ-4--used-in-mstape-inf-to-load-mstape-sys-"></a>**AVC \\即使 \_ 50F2&TYP \_ 4** (在 *Mstape* 中用于加载 *Mstape.sys*)   

<a href="" id="avc-typ-4"></a>**AVC \\ TYP \_ 4**  

-   在 INF 文件中，调谐器子单位的 (其中 **_SubunitType_* _ = 5) 设备标识符将显示为：

<a href="" id="avc-ven-50f2-mod-0-typ-5-id-0"></a>_ *AVC \\ 即使 \_ 50F2&MOD \_ 0&TYP \_ 5&ID \_ 0**  

-   调谐器子单位的兼容标识符为：

<a href="" id="avc-ven-50f2-mod-0-typ-5"></a>**AVC \\ 即使 \_ 50F2&MOD \_ 0&TYP \_ 5**  

<a href="" id="avc-ven-50f2-typ-5"></a>**AVC \\ 即使 \_ 50F2&TYP \_ 5**  

<a href="" id="avc-typ-5"></a>**AVC \\ TYP \_ 5**  

**注意**  ：供应商只应在上述情况下指定硬件标识符，并且决不要指定兼容的标识符。 而且，供应商不应提供与 Microsoft 提供的 INF 文件中的标识符相匹配的任何设备标识符。

 

 

 




