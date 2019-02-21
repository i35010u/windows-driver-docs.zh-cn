---
title: 安装自定义即插即用打印机驱动程序
description: 安装自定义即插即用打印机驱动程序
ms.assetid: 0269afbe-c7d1-4227-ad77-b921852d6a0c
keywords:
- 自定义打印机驱动程序 WDK，插
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3124b506928018a113461baae3bb1b197431bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546229"
---
# <a name="installing-a-custom-plug-and-play-printer-driver"></a>安装自定义即插即用打印机驱动程序





在 Windows XP 上的插管理器加载驱动程序按此顺序 （从最高到最低的首选项进行列出）：

1.  签名的 IHV 驱动程序

2.  "现成"驱动程序

3.  未签名的 IHV 驱动程序

在 Windows 2000 上没有现成和签名 IHV 驱动程序之间没有区别： 驱动程序的任何一种加载优先于未签名的 IHV 驱动程序。 若要了解有关用于安装驱动程序和替换"现成"驱动程序的 INF 文件的应用程序的详细信息，请参阅[编写设备安装应用程序](https://msdn.microsoft.com/library/windows/hardware/ff554015)。

如果你正在开发的驱动程序，取代了 Windows 2000 现成驱动程序，请确保*硬件 Id*中[ **INF 模型部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)的 INF 文件包含相应的端口的枚举器。 Ntprint.inf 的 Windows 2000 版本在其 INF 模型节中的项包括端口枚举器。 如果相同的条目 INF 文件中省略端口枚举器，插选择优先于您的现成 Windows 2000 驱动程序。 如果您的驱动程序取代 Windows XP 现成驱动程序，无需包括端口枚举器中的硬件 id。

IHV 可以避免对话框，询问有关客户端安装中的用户交互通过为每个模型，如以下示例所示提供 INF 模型部分中的两行。

```cpp
; Models section

[OEM Company Name]
"XYZ PScript Printer" = OEMXYZ.PPD, LPTENUM\OEM_Company_NameXYZ_F84F, XYZ_PScript_Printer
"XYZ PScript Printer" = OEMXYZ.PPD, OEM_Company_NameXYZ_F84F, XYZ_PScript_Printer
.
.
.
```

在此示例中，两行都几乎完全相同，仅不同总线枚举器 (LPTENUM) 包含在第一行中的硬件 ID。 在每个行中，第二个和第三个条目的值分别为硬件 ID 和兼容 ID。 通过特定的总线 （在本例中的并行端口） 安装的打印机，在第一行中的硬件 ID 生成硬件 ID 匹配，这是最可能的匹配项。 对于通过其他总线安装打印机，第二行中的硬件 ID 还将生成的硬件 ID 匹配项。

在任一情况下，安装程序不需要来自上是否安装该驱动程序，因此不会显示一个对话框，要求作出响应的用户的响应。 但请注意，如果不匹配则硬件 ID 匹配项，而*兼容 ID*匹配项，而安装发生在客户端安装程序将显示对话框，询问用户交互。

 

 




