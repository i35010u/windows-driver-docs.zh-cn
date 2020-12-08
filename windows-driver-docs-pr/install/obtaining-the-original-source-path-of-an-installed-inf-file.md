---
title: 获取已安装 INF 文件的原始源路径
description: 获取已安装 INF 文件的原始源路径
keywords:
- Setupapi.log 函数 WDK，INF 文件
- 路径 WDK Setupapi.log
- INF 文件 WDK Setupapi.log
- 源路径 WDK INF 文件
- 原始源路径 WDK INF 文件
- 正在检索 INF 文件路径信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5104988fbb3d41f412356541278cee4e8935c4ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839077"
---
# <a name="obtaining-the-original-source-path-of-an-installed-inf-file"></a>获取已安装 INF 文件的原始源路径


本主题介绍如何检索系统 INF 目录中安装的 INF 文件的原始源路径。 尽管不存在直接执行此检索的 [setupapi.log](setupapi.md) 函数，但你可以通过在 INF 文件中包含条目来间接执行检索，以便访问 inf 文件条目的 setupapi.log 函数可以用于检索已安装的 inf 文件中的原始源路径信息。

此方法仅适用于在系统 INF 文件目录中安装的 INF 文件。 不能将此方法用于 [驱动程序存储区](driver-store.md)中存在的 INF 文件。

随 Windows 驱动程序工具包中的 toaster 示例一起提供的共同安装程序 (WDK) 使用此方法，本主题包括 toaster 示例中的摘录，其中显示了此方法。 有关 toaster 示例的详细信息，请参阅 WDK 的 *src \\ general \\ toaster* 目录中提供的 *toasterpkg.htm*。

若要使用此方法检索已安装 INF 文件的原始源路径，请执行以下操作：

1.  在 INF 文件中包含一个节，其中包含一个项，其第一个字段是 %1% 字符串密钥标记。 默认情况下，%1% string key 标记表示 INF 文件的原始源路径。 当 Windows 安装此类 INF 文件时，它会将原始源路径字符串与 INF 文件的已安装版本保存在一起。 请注意，此方法仅适用于使用 %1% 的情况，如本示例中所示。 通常，%1% 解析为依赖于上下文的。 例如，在 " *添加注册表" 部分* 输入中的 %1% 字段不会解析为原始源路径;相反，此上下文中的 %1% 解析为 [驱动程序存储区](driver-store.md)中对应 INF 文件的路径。

2.  使用 **SetupOpenInfFile**、 **SetupFindFirstLine** 和 **SetupGetStringField** 从包含 %1% string key 标记的条目中检索原始源路径。

例如， *toasterpkg* 包含以下 \[ ToasterCoInfo 节，其中包含 \] 第一个字段为 %1% string key 标记的自定义 OriginalInfSourcePath 项。

```cpp
[ToastCoInfo]
; Used by the toaster co-installer to figure out where the original media is
; located (so it can start value-added setup programs).
OriginalInfSourcePath = %1%
```

如果 INF 按 toaster 示例所示进行配置，则可以在系统 INF 目录中安装 INF 文件后检索原始源路径。 若要检索原始源路径，请首先调用 **SetupOpenInfFile** 以打开已安装的 INF 文件。 例如， *toastco* 中的以下代码示例将打开安装的 *toasterpkg* 文件。

```cpp
// Since the INF is already in %SystemRoot%\Inf, we need to find out where it
// originally came from.  There is no direct way to ascertain an INF's
// path of origin, but we can indirectly determine it by retrieving a field
// from our INF that uses a string substitution of %1% (DIRID_SRCPATH).
//
hInf = SetupOpenInfFile(DriverInfoDetailData->InfFileName,
                        NULL,
                        INF_STYLE_WIN4,
                        NULL
                        );
```

打开已安装的 INF 文件后，调用 **SetupFindFirstLine** 来检索包含其第一个字段为 %1% string key 标记的条目的部分的第一行。 接下来，调用 **SetupGetStringField** 检索此项的第一个字段，并检索 INF 文件的原始源路径。 例如， *toastco* 中的以下代码示例检索包含自定义 OriginalInfSourcePath 条目的行，然后检索此项的第一个字段。 由于原始 INF 中的第一个字段是 %1% string key 标记，因此 **SetupGetStringField** 返回 INF 文件的原始源路径。

```cpp
// Contained within our INF should be a [ToastCoInfo] section with the
// following entry:
//
//     OriginalInfSourcePath = %1%
//
// If we retrieve the value (i.e., field 1) of this line, we'll get the
// full path where the INF originally came from.
//
if(!SetupFindFirstLine(hInf, L"ToastCoInfo", L"OriginalInfSourcePath", &InfContext)) {
   goto clean0;
}
if(!SetupGetStringField(&InfContext, 1, *MediaRootDirectory, MAX_PATH, &PathLength) ||
  (PathLength <= 1)) {
  goto clean0;
```

 

 





