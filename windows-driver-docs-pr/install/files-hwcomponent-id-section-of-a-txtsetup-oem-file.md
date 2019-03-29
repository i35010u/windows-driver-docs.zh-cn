---
title: TxtSetup.oem 文件的 Files.HwComponent.ID 节
description: Files.HwComponent.ID 部分列出了如果用户选择特定组件选项复制的文件。 这些部分之一必须存在的每个 HwComponent 部分中列出每个选项。
ms.assetid: a2c48a94-18a9-4efe-bdff-6c08bbbbabf9
keywords:
- Files.HwComponent.ID 部分中的 TxtSetup.oem 文件的设备和驱动程序安装
topic_type:
- apiref
api_name:
- Files.HwComponent.ID Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 92e6b773f0ae1377c51d76990863154c61b435ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566608"
---
# <a name="fileshwcomponentid-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Files.HwComponent.ID 节


一个**文件。**<em>HwComponent</em>**。**<em>ID</em>部分列出了如果用户选择特定组件选项复制的文件。 这些部分之一必须存在每个选项中各*HwComponent*部分。

``` syntax
[Files.HwComponent.ID]
filetype = diskN,filename[,DriverKey]
...
```

<a href="" id="files-hwcomponent-id"></a>**文件。** <em>HwComponent</em>**。**<em>ID</em>  
*HwComponent*的名称对应*HwComponent*文件中的部分。 *ID*对应于*ID*中的条目*HwComponent*部分。

<a href="" id="filetype"></a>*filetype*  
标识要复制的文件的类型。 这些条目之一是为每个文件要复制此存在*HwComponent*。*ID*。

*Filetype*是系统定义的以下值之一：

<a href="" id="driver"></a>**driver**  
有效的所有组件。 Windows 会将文件复制到 %*systemroot %\\system32\\驱动程序。*

<a href="" id="dll"></a>**dll**  
有效的所有组件。 对于显示驱动程序的 GDI 部分很有用。 Windows 会将文件复制到 %*systemroot %\\system32。*

<a href="" id="hal"></a>**hal**  
仅对有效**计算机**组件。 Windows 会将文件复制到 %*systemroot %\\system32\\hal.dll* （对于 x86) 或设置为 *\\os\\winnt\\hal.dll*系统上分区 （适用于非 x86)。

<a href="" id="inf"></a>**inf**  
有效的所有组件。 指定设备的常规 INF 文件。 此文件用于在 GUI 模式下安装过程和其他设备维护操作。 将文件复制到 %*systemroot %\\system32*。

<a href="" id="catalog"></a>**catalog**  
对驱动程序有效。 指定设备的目录文件。 无需进行任何组件。 例如，**目录**= d1 *mydriver.cat*。 请参阅有关目录文件的详细信息的 WHQL 准则。

<a href="" id="detect"></a>**detect**  
对有效**计算机**组件 (仅限 x86)。 如果指定，则替换标准 x86 硬件识别器。 Windows 将文件复制到*c:\\ntdetect.com*。

<a href="" id="diskn"></a>*diskN*  
标识要从其中复制文件的磁盘。 此值必须匹配中的条目**磁盘**部分。

<a href="" id="filename"></a>*filename*  
指定文件，不包括目录路径或驱动器的名称。 若要形成文件的完整名称，Windows 将追加*文件名*中的磁盘指定的目录**磁盘**部分。 文件的名称不能超过八个字符，并扩展不能超过三个字符。

<a href="" id="driverkey"></a>*DriverKey*  
指定要在此文件中，注册表服务树中创建的键的名称，如果该文件的类型**驱动程序**。 此值用于窗体**配置。**<em>DriverKey</em>部分名称。 此值是必需的组件的类型**scsi**。

下面的示例演示**文件。**<em>HwComponent</em>**。**<em>ID</em>主题中*TxtSetup.oem*文件：

``` syntax
; ...
[Files.SCSI.oemscsi]
driver = d1,oemfs2.sys,OEMSCSI
inf = d1,oemsetup.inf
dll = d1, oemdrv.dll
catalog = d1, oemdrv.cat
; ...
```

 

 





