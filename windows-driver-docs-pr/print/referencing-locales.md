---
title: 引用的区域设置
description: 引用的区域设置
ms.assetid: 63ea5534-b2e1-43aa-b45b-e4fe8bb69f49
keywords:
- Unidrv，引用区域设置
- GPD 文件 WDK Unidrv，引用区域设置
- 引用的区域设置
- 引用 WDK Unidrv 的区域设置
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a47fe10eb8df01764acd99b04967442bc3ee7e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567496"
---
# <a name="referencing-locales"></a>引用的区域设置





### <a name="using-gpd-files"></a>使用 GPD 文件

GPD 文件可以引用系统的区域设置。 通常情况下，在使用区域设置标识符\*Switch 的语句，其中参数，如默认纸张大小和资源 Dll 中可以指定以区域设置特定的方式。

若要引用的区域设置信息，GPD 文件必须包含\*包括包含文件 locale.gpd 语句 (其中提供使用 Windows 驱动程序工具包\[WDK\])，如下所示：

```cpp
*Include: locale.gpd
```

此 GPD 文件定义一个名为"区域设置"功能，并定义多个区域设置的选项。 （请参阅文件以查看定义的区域设置。）下面是这些区域设置选项的用法示例。 该示例将访问的区域设置的默认纸张大小。

```cpp
*Feature: PaperSize
{
...
    Option: A4
    {
    }
    ...
*switch: Locale
{
    *case: English_United_States
    {
        *DefaultOption: Letter
    }
    *case: English_United_Kingdom
    {
        *DefaultOption: A4
    }
    *default:
    {
        *DefaultOption: Letter
    }
} *% End of switch
} *% End of Feature: PaperSize
```

在运行时，Unidrv 确定系统的默认区域设置通过调用**GetSystemDefaultLCID** （Microsoft Windows SDK 文档中所述）。 安装打印机时，GPD 分析器读取打印机的 GPD 文件，并使用中的信息\*Case 语句与默认区域设置相关联。 （请注意，是否安装打印机后更改系统区域设置，基于区域设置的选项不会更改。）

下面是另一个示例中，选择 DLL 根据区域设置的资源。 资源 DLL 可以包含特定于区域设置的资源，例如显示字符串。

```cpp
*switch: Locale
{
    *case: English_United_States
    {
        *ResourceDLL: english.dll
    }
    *case: German_Standard
    {
        *ResourceDLL: german.dll
    }
    *default:
    {
        *ResourceDLL: english.dll
    }
}
```

### <a name="setting-default-paper-size-by-locale"></a>设置由区域设置的默认纸张大小

您可能想要将驱动程序分配的默认纸张大小，度量值或非度量值，根据用户的地理位置。

下面的算法检索默认系统区域设置，然后使用国家/地区代码来确定系统区域设置是否表示通常使用度量值或非度量值的纸张大小的国家/地区。 使用此信息，您的驱动程序可以设置的默认纸张大小相应地，如 A4 国家/地区使用公制的和不的国家/地区的信纸大小。

1.  使用[GetLocaleInfo](https://go.microsoft.com/fwlink/p/?linkid=52069)函数 （在 Microsoft Windows SDK 文档中定义） 来检索默认系统区域设置。 使用区域设置\_系统\_的第一个参数，默认*区域设置*，和区域设置\_对于第二个参数，ICOUNTRY *LCType*。

2.  使用默认系统区域设置从获取**GetLocaleInfo**来确定度量值或非度量值的纸张大小。
    -   非-指标如果默认系统区域设置是：
        -   CTRY\_UNITED\_状态，或
        -   CTRY\_加拿大，或
        -   大于或等于 50 个，但不超过 60 和不 CTRY\_巴西，或
        -   大于或等于 500，但小于 600
    -   否则为的度量值。

 

 




