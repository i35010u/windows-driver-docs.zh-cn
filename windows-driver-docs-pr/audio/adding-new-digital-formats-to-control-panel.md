---
title: 向控制面板添加新的数字格式
description: 向控制面板添加新的数字格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9db331771f7210066d470aecce3d08771aa1748
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785037"
---
# <a name="adding-new-digital-formats-to-control-panel"></a>向控制面板添加新的数字格式


在 Windows Vista 和更高版本的 Windows 中，你可以开发通过 SPDIF 流式传输并使其在 "控制面板" 中可用的第三方数字音频格式。

开发数字音频格式后，为格式定义新的 GUID，并使用 INF 文件来安装关联的音频驱动程序。 INF 文件中的以下代码显示了如何将有关新数字音频格式的必要信息添加到注册表中：

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

在前面的示例中，"字符串" 部分中显示的 GUID \[ \] 用于说明为新数字格式定义的 guid 的位置。 HKLM 用作 HKEY 本地计算机的标准缩写 \_ \_ 。

**重要提示**  Mycion 和 Testfile.txt 的两个 HKLM 行条目都是必需的。 "C： \\ Program Files \\ MyVendor \\ " 文件夹已用于显示您必须为与驱动程序相关的图标和测试波形文件创建相应的文件夹。

 

 

 




