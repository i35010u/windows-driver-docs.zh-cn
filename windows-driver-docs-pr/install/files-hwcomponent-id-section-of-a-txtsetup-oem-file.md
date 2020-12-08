---
title: TxtSetup.oem 文件的 Files.HwComponent.ID 节
description: Files.HwComponent.ID 部分列出了用户选择特定组件选项时要复制的文件。 必须为每个 HwComponent 部分中列出的每个选项提供这些部分中的一节。
keywords:
- Txtsetup.oem 文件设备和驱动程序安装的 Files.HwComponent.ID 部分
topic_type:
- apiref
api_name:
- Files.HwComponent.ID Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4a933cc6a36c700c0d9de012c9c4723e5cbac88b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824449"
---
# <a name="fileshwcomponentid-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Files.HwComponent.ID 节


**文件。**<em>HwComponent</em>**。**<em>ID</em>部分列出了用户选择特定组件选项时要复制的文件。 必须为每个 *HwComponent* 部分中列出的每个选项提供这些部分中的一节。

``` syntax
[Files.HwComponent.ID]
filetype = diskN,filename[,DriverKey]
...
```

<a href="" id="files-hwcomponent-id"></a>**文件。**<em>HwComponent</em>**。**<em>ID</em>  
*HwComponent* 对应于文件中 *HwComponent* 部分的名称。 *Id* 对应于该 *HwComponent* 部分中的 *id* 条目。

<a href="" id="filetype"></a>*filetype*  
标识要复制的文件的类型。 为此 *HwComponent* 复制的每个文件都存在其中一个条目。*ID*。

" *类型* " 是下列系统定义的值之一：

<a href="" id="driver"></a>**驱动器**  
对于所有组件都有效。 Windows 将该文件复制到%*systemroot% \\ system32 \\ 驱动程序。*

<a href="" id="dll"></a>**.dll**  
对于所有组件都有效。 适用于显示驱动程序的 GDI 部分。 Windows 将该文件复制到%*systemroot% \\ system32 中。*

<a href="" id="hal"></a>**hal**  
仅对 **计算机** 组件有效。 对于非 x86 (，Windows 将文件复制到%*systemroot% \\ system32 \\hal.dll* (用于 x86) 或操作系统分区 *\\ \\ \\hal.dll* 上的操作系统。

<a href="" id="inf"></a>**遵从**  
对于所有组件都有效。 指定设备的常规 INF 文件。 此文件用于 GUI 模式安装过程中以及其他设备维护操作。 文件将复制到%*systemroot% \\ system32* 中。

<a href="" id="catalog"></a>**分类**  
对驱动程序有效。 指定设备的目录文件。 对于任何组件都不需要。 例如， **目录** = d1， *mydriver.cat*。 有关编录文件的详细信息，请参阅 WHQL 指导原则。

<a href="" id="detect"></a>**察觉**  
仅)  (x86 的 **计算机** 组件。 如果已指定，则替换标准 x86 硬件识别器。 Windows 将文件复制到 *c： \\ ntdetect.com*。

<a href="" id="diskn"></a>*diskN*  
标识要从其复制文件的磁盘。 此值必须与 " **磁盘** " 部分中的条目相匹配。

<a href="" id="filename"></a>*名字*  
指定文件的名称，不包括目录路径或驱动器。 为了形成完整的文件名，Windows 会将 *文件名* 附加到在 " **磁盘** " 部分中为磁盘指定的目录。 文件名不得超过八个字符，且扩展名不得超过三个字符。

<a href="" id="driverkey"></a>*DriverKey*  
如果文件为 **驱动程序** 类型，则指定要在此文件的注册表服务树中创建的密钥的名称。 此值用于形成 **Config。**<em>DriverKey</em> 部分名称。 对于 **scsi** 类型的组件，此值是必需的。

下面的示例演示了一个 **文件。**<em>HwComponent</em>**。***Txtsetup.oem* 文件中的 <em>ID</em>部分：

``` syntax
; ...
[Files.SCSI.oemscsi]
driver = d1,oemfs2.sys,OEMSCSI
inf = d1,oemsetup.inf
dll = d1, oemdrv.dll
catalog = d1, oemdrv.cat
; ...
```

 

 





