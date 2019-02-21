---
title: 添加新的数字格式都移到控件面板
description: 添加新的数字格式都移到控件面板
ms.assetid: ce36738c-6471-4b68-82ad-80b8509c052b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f063c2d35dc62e8d9310a0adbfdc8b2b4f58908
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556126"
---
# <a name="adding-new-digital-formats-to-control-panel"></a>添加新的数字格式都移到控件面板


在 Windows Vista 和更高版本的 Windows 中，可以通过 SPDIF 开发第三方的数字音频格式，以流式传输，并使此格式在控制面板中可用。

开发您的数字音频格式后，定义新的 GUID 格式，并使用 INF 文件来安装关联的音频驱动程序。 INF 文件中的以下代码演示如何将有关新数字音频格式的必要信息添加到注册表：

```inf
[Version]
Signature=$WindowsNT$
...
[DDInstall]
AddReg = AddReg.NewDigitalFormat
...
...
[AddReg.NewDigitalFormat]
HKLM, %My_SubKey%, "DisplayName",,"ABC Audio"
HKLM, %My_SubKey%, "CustomIcon",,"c:\Program Files\MyVendor\myicon.ico"
HKLM, %My_SubKey%, "TestFile",,"c:\Program Files\MyVendor\testfile.wav"
...
[Strings]
My_SubKey = "SOFTWARE\Microsoft\Windows\CurrentVersion\MMDevices\SPDIF_Formats\{00000682-0000-0010-8000-00aa00389b71}"
...
...
```

在前面的示例中所示的 GUID\[字符串\]部分用于说明为新的数字格式定义的 GUID 的位置。 HKLM 用作标准的缩写 HKEY\_本地\_机。

**重要**  Mycion.ico 和 Testfile.wav 的两个 HKLM 行项所需。 "C:\\Program Files\\MyVendor\\"使用文件夹以显示你必须为您的驱动程序相关图标创建相应的文件夹和测试批文件。

 

 

 




