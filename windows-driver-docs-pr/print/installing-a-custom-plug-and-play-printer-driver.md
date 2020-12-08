---
title: 安装自定义的即插即用打印机驱动程序
description: 安装自定义的即插即用打印机驱动程序
keywords:
- 自定义打印机驱动程序 WDK，即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 343bdcd52ca37765ae4fdaf8dfc3cb781ae3a445
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796733"
---
# <a name="installing-a-custom-plug-and-play-printer-driver"></a>安装自定义的即插即用打印机驱动程序





在 Windows XP 中，即插即用管理器按此顺序加载驱动程序， (从最高到最低的首选项) 列出：

1.  签名 IHV 驱动程序

2.  "机箱内" 驱动程序

3.  无符号 IHV 驱动程序

在 Windows 2000 上，机箱内和签名的 IHV 驱动程序之间没有区别：任何一种类型的驱动程序都按优先顺序加载到无符号的 IHV 驱动程序中。 若要详细了解设计用于安装替代 "内置" 驱动程序的驱动程序和 INF 文件的应用程序，请参阅 [编写设备安装应用程序](../install/writing-a-device-installation-application.md)。

如果要开发替换 Windows 2000 内置驱动程序的驱动程序，请确保 INF 文件的 " [**Inf 模型" 部分**](../install/inf-models-section.md)中的 *硬件 id* 包含相应的端口枚举器。 Windows 2000 版本的 Ntprint.inf 在 INF 模型部分的条目中包含端口枚举器。 如果 INF 文件中的相同项省略端口枚举器，即插即用会按优先选择的内置 Windows 2000 驱动程序。 如果驱动程序替换了 Windows XP 内置驱动程序，则无需在硬件 ID 中包含端口枚举器。

在每个模型的 "INF 模型" 部分中提供两行，IHV 可以避免在客户端安装中请求用户交互的对话框，如以下示例中所示。

```cpp
; Models section

[OEM Company Name]
"XYZ PScript Printer" = OEMXYZ.PPD, LPTENUM\OEM_Company_NameXYZ_F84F, XYZ_PScript_Printer
"XYZ PScript Printer" = OEMXYZ.PPD, OEM_Company_NameXYZ_F84F, XYZ_PScript_Printer
.
.
.
```

在此示例中，这两行几乎完全相同，只是在第一行的硬件 ID 中包含了总线枚举器 (LPTENUM) 。 每行中的第二个和第三个条目值分别分别为硬件 ID 和兼容 ID。 对于在这种情况下 (并行端口安装在特定总线上的打印机) ，第一行中的硬件 ID 会生成硬件 ID 匹配项，这是最佳的可能匹配项。 对于通过任何其他总线安装的打印机，第二行中的硬件 ID 还会生成硬件 ID 匹配。

在这两种情况下，安装程序不需要用户提供有关是否安装驱动程序的响应，因此不会显示请求响应的对话框。 但请注意，如果匹配不是硬件 ID 匹配项，而是 *兼容的 id* 匹配，则在客户端进行安装，则安装程序会显示一个对话框，要求用户交互。

 

