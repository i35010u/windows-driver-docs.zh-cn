---
title: 在 Visual Studio 中配置异常和事件
description: 你可以配置 Windows 调试器以预先确定的方式对指定的异常和事件做出反应。 对于每个异常，可以设置中断状态和处理状态。
ms.assetid: 531CFE28-B0DA-4B6D-896F-C8F678C7FE00
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f02524a52c849b5586ea8f9c2e4735d759df060
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367002"
---
# <a name="configuring-exceptions-and-events-in-visual-studio"></a>在 Visual Studio 中配置异常和事件

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>


你可以配置 Windows 调试器以预先确定的方式对指定的异常和事件做出反应。 对于每个异常，可以设置中断状态和处理状态。 对于每个事件，可以设置中断状态。

本主题中所示的步骤要求具有集成到 Visual Studio Windows 驱动程序工具包。 要获取的集成的环境，请首先安装 Microsoft Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows 驱动程序开发](https://docs.microsoft.com/windows-hardware/drivers/)。

可以通过在调试器的即时窗口中输入以下命令配置的中断状态或处理状态。 如果尚未打开，请在调试器即时窗口**调试**菜单中，选择**Windows&gt;即时**。

-   [**sxe**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)
-   [**sxd**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)
-   [**sxn**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)
-   [**sxi**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)

有关异常和事件的详细讨论，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

 

 





