---
title: 获取已安装的 INF 文件的原始源路径
description: 获取已安装的 INF 文件的原始源路径
ms.assetid: 7e086248-b11d-43ee-9afa-fad6f2136dc8
keywords:
- 安装程序 Api 函数 WDK、 INF 文件
- 路径 WDK SetupAPI
- INF 文件 WDK SetupAPI
- 源路径 WDK INF 文件
- 原始源路径 WDK INF 文件
- 检索 INF 文件路径信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80dfb06f68c302192eac513f6d71153767738a2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524939"
---
# <a name="obtaining-the-original-source-path-of-an-installed-inf-file"></a>获取已安装的 INF 文件的原始源路径


本主题介绍如何检索系统 INF 目录中安装的 INF 文件的原始源路径。 尽管没有任何[SetupAPI](setupapi.md)函数直接执行此检索中，您可以通过在 INF 文件中包含的条目，以便访问 INF 文件条目的安装程序 Api 函数可以用于检索间接执行检索已安装的 INF 文件中的原始源路径信息。

此方法仅适用于系统 INF 文件目录中安装的 INF 文件。 不能使用此方法的 INF 文件中存在[驱动程序存储区](driver-store.md)。

Windows Driver Kit (WDK) 中的 toaster 示例提供共同安装程序使用此方法和本主题包括部分内容摘自 toaster 示例演示此方法。 有关 toaster 示例的详细信息，请参阅*toasterpkg.htm*，在提供*src\\常规\\toaster* WDK 的目录。

若要使用此方法检索已安装的 INF 文件的原始源路径，请执行以下操作：

1.  INF 文件中包含一个部分，其中包括其第一个字段是 %1%字符串键标记的条目。 默认情况下，%1%字符串密钥令牌表示 INF 文件的原始源的路径。 Windows 安装时此类的 INF 文件，它将与已安装的 INF 文件保存原始源路径字符串。 请注意，此方法仅适用如果 %1%已使用在此示例中所示。 一般情况下，%1%解析为与上下文相关。 例如，%1%中的字段*添加注册表部分*条目未解析为原始的源路径; 而是在此上下文中的 %1%解析为相应的 INF 文件中的路径[驱动程序存储区](driver-store.md)。

2.  使用**SetupOpenInfFile**， **SetupFindFirstLine**，并**SetupGetStringField**检索包括 %1%字符串键标记的项的原始源路径。

例如， *toasterpkg.inf*包含了下列\[ToasterCoInfo\]节替换其第一个字段是 %1%字符串密钥令牌的自定义 OriginalInfSourcePath 条目。

```cpp
[ToastCoInfo]
; Used by the toaster co-installer to figure out where the original media is
; located (so it can start value-added setup programs).
OriginalInfSourcePath = %1%
```

如果 INF 配置 toaster 示例所示，然后可以检索在系统 INF 目录中安装的 INF 文件后的原始源路径。 若要检索的原始源路径，将第一次调用**SetupOpenInfFile**打开已安装的 INF 文件。 例如，下面的代码示例从*toastco.c*将打开已安装*toasterpkg.inf*文件。

```cpp
// Since the INF is already in %SystemRoot%\Inf, we need to find out where it
// originally came from.  There is no direct way to ascertain an INF&#39;s
// path of origin, but we can indirectly determine it by retrieving a field
// from our INF that uses a string substitution of %1% (DIRID_SRCPATH).
//
hInf = SetupOpenInfFile(DriverInfoDetailData->InfFileName,
                        NULL,
                        INF_STYLE_WIN4,
                        NULL
                        );
```

打开已安装的 INF 文件后，调用**SetupFindFirstLine**来检索包含其第一个字段是 %1%字符串键标记的项的部分的第一行。 接下来，调用**SetupGetStringField**来检索此项的第一个字段，并检索 INF 文件的原始源路径。 例如，下面的代码示例从*toastco.c*检索包含自定义 OriginalInfSourcePath 条目，然后检索此项的第一个字段的行。 原始 INF 的第一个字段是 %1%字符串密钥令牌，因为**SetupGetStringField**返回 INF 文件的原始源路径。

```cpp
// Contained within our INF should be a [ToastCoInfo] section with the
// following entry:
//
//     OriginalInfSourcePath = %1%
//
// If we retrieve the value (i.e., field 1) of this line, we&#39;ll get the
// full path where the INF originally came from.
//
if(!SetupFindFirstLine(hInf, L"ToastCoInfo", L"OriginalInfSourcePath", &InfContext)) {
   goto clean0;
}
if(!SetupGetStringField(&InfContext, 1, *MediaRootDirectory, MAX_PATH, &PathLength) ||
  (PathLength <= 1)) {
  goto clean0;
```

 

 





