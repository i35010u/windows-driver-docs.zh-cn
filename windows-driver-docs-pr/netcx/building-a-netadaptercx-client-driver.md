---
title: 生成 NetAdapterCx 客户端驱动程序
description: 生成 NetAdapterCx 客户端驱动程序
ms.assetid: 0A6957B4-E63A-4687-B31E-064AE3A34936
keywords:
- 生成 NetAdapterCx 客户端驱动程序，构建 NIC 驱动程序
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: a340ed692cdf373b50c311aef8623e437422c353
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386376"
---
# <a name="building-a-netadaptercx-client-driver"></a>生成 NetAdapterCx 客户端驱动程序

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

若要获取最新版本的 Visual Studio 和 Windows Driver Kit (WDK)，请访问[硬件开发人员中心](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

使用以下步骤在 Visual Studio 中创建新的 NetAdapter 客户端驱动程序：

1. 打开 Microsoft Visual Studio。 在文件菜单上依次选择**新建 > 项目**。
2. 在中**新建项目 > 模板 > Visual C++ > Windows 驱动程序 > WDF**对话框中，选择**内核模式驱动程序 (KMDF) 模板**。
3. 若要打开驱动程序属性页对话框中，选择**项目 > 属性**。
4. 在中**配置属性 > 驱动程序设置 > 网络适配器驱动程序**对话框中，选择**链接至网络适配器类扩展**下拉列表中并将设置为**是**.
5. 在中**配置属性 > 驱动程序设置 > 网络适配器驱动程序**对话框中，选择**网络适配器的主要版本**和**网络适配器的次要版本**.
    1. 是当前版本的 NetAdapterCx **1.3**。
6. 将以下标头添加到每个源文件 （或你常见/预编译标头）：

```C++
#include <ntddk.h>
#include <wdf.h>
#include <netadaptercx.h>
```

若要观看的视频，演示如何在 Visual Studio 中创建新的 NetAdapter 客户端驱动程序，请参阅[网络适配器类扩展：第一个驱动程序](https://aka.ms/netadapter/video2)第 9 频道上的视频。
