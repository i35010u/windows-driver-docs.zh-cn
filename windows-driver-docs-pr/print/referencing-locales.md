---
title: 引用的区域设置
description: 引用的区域设置
ms.assetid: 63ea5534-b2e1-43aa-b45b-e4fe8bb69f49
keywords:
- Unidrv，引用区域设置
- GPD 文件 WDK Unidrv，引用区域设置
- 引用区域设置
- 引用 WDK Unidrv 的区域设置
- Unidrv WDK 打印
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: d995b24d21a53624bfb94344384ad5e1146cfdff
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756169"
---
# <a name="referencing-locales"></a>引用区域设置

## <a name="using-gpd-files"></a>使用 GPD 文件

GPD 文件可以引用系统的区域设置。 通常，在 Switch 语句中使用区域设置标识符 \* ，其中的参数（例如，默认的纸张大小和资源 dll）可以通过特定于区域设置的方式指定。

若要引用区域设置信息，GPD 文件必须包含包含 \* 文件区域设置的 Include 语句，其中包含 Windows 驱动程序工具包（WDK），如下所示：

```cpp
*Include: locale.gpd
```

此 GPD 文件定义了一个名为 "Locale" 的功能，并为许多区域设置定义了选项。 （请参阅文件以查看定义了哪些区域设置。）下面是这些区域设置选项的示例用法。 该示例基于区域设置的默认纸张大小。

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

在运行时，Unidrv 通过调用**GetSystemDefaultLCID**确定系统的默认区域设置（如 Microsoft Windows SDK 文档中所述）。 安装打印机时，GPD 分析器读取打印机的 GPD 文件，并使用 \* 与默认区域设置关联的 Case 语句中的信息。 （请注意，如果在安装打印机后更改了系统的区域设置，则不会更改基于区域设置的选项。）

下面是另一个示例，该示例选择基于区域设置的资源 DLL。 资源 DLL 可包含特定于区域设置的资源，如显示字符串。

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

## <a name="setting-default-paper-size-by-locale"></a>按区域设置设置默认纸张大小

您可能想要让您的驱动程序根据用户的地理位置分配默认纸张大小（公制或非度量值）。

以下算法检索默认的系统区域设置，然后使用国家/地区代码来确定系统区域设置是否表示一个通常使用度量或非指标纸张大小的国家/地区。 使用此信息，您的驱动程序可以相应地设置默认纸张大小，例如，对于使用度量系统的国家/地区，使用不是的国家/地区的 A4。

1. 使用[GetLocaleInfo](https://docs.microsoft.com/previous-versions//ms776270(v=vs.85))函数检索默认的系统区域设置。 对于第 \_ 一个参数，请使用区域设置系统 \_ 默认值，为第二个参数使用*区域设置* \_ ICOUNTRY，为*LCType*。

1. 使用从**GetLocaleInfo**获取的默认系统区域设置来确定度量或非指标纸张大小。
    - 非度量值（如果默认的系统区域设置为：

        - CTRY \_ \_ 或

        - \_加拿大 CTRY

        - 大于或等于50，但小于60而不是 CTRY \_ 巴西或

        - 大于或等于500，但小于600

    - 否则为指标。
