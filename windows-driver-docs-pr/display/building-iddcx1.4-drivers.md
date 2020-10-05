---
title: 构建 IddCx 1.4 驱动程序
description: 如何生成 IddCx 版本1.4 间接显示驱动程序
ms.assetid: 4e065381-f1cd-401a-9844-f85eaf414b5f
ms.date: 09/28/2020
keywords:
- 生成间接显示驱动程序，版本1。4
- 生成 IDDs，版本1。4
ms.localizationpriority: medium
ms.openlocfilehash: 509bec15f5bc608f60a497cbee3c8831696ef22d
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734303"
---
# <a name="building-iddcx-14-drivers"></a>构建 IddCx 1.4 驱动程序

由于在 IddCx 1.3 for Windows 10 版本1809中所做的更改，基于 IddCx v2.0 构建的 (IDD) 的间接显示器驱动程序可以在 Windows 10 版本1809上运行，并使用运行时检查来验证 IddCx 1.4 中的 DDI 更改在该系统上是否可用。 有关详细信息，请参阅为 [多个版本的 Windows 构建 WDF 驱动程序](../wdf/building-a-wdf-driver-for-multiple-versions-of-windows.md) 。

从 IddCx 1.4 开始，可通过执行以下操作，构建 IddCx 驱动程序，以便在 Windows 10 版本1803及更高版本上安装。 注意：此驱动程序不会在 Windows 10 版本1607到1709上加载。

* 使用 [Windows 驱动程序工具包](../download-the-wdk.md) (WDK) 中的 IddCx 1.4 标头和库，生成和链接驱动程序。
* 在生成环境中将 IDDCX_MINIMUM_VERSION_REQUIRED 设置为3。 这会告知操作系统生成驱动程序所用的最低 IddCx 版本，在本例中为1.3。
* 初始化 IddCx 结构时，请使用相应的 *XXX*_INIT 宏。 例如，使用 IDD_CX_CLIENT_CONFIG_INIT ( # A1 宏来初始化 IDD_CX_CLIENT_CONFIG 结构。 宏使用运行时代码将 "大小" 字段设置为运行驱动程序的 IddCx 版本的正确大小。
* 使用 IDD_IS_FIELD_AVAILABLE ( # A1 宏来确定从 IddCx 传递到驱动程序的结构是否已定义该字段。 注意： IddCx 1.4 未将从 IddCx 传递的任何现有结构扩展到驱动程序，因此不需要在 IddCx 1.4 中使用此宏。
* 使用 IDD_IS_FUNCTION_AVAILABLE ( # A1 宏来确定给定的 IddCx 函数在运行驱动程序的操作系统上是否可用。 例如，使用 IDD_IS_FUNCTION_AVAILABLE (IddCxAdapterSetRenderAdapter) 来确定此操作系统是否支持 IddCxAdapterSetRenderAdapter ( # A3。

下表汇总了不同 OS 版本支持的 IddCx 版本。

| OS 版本。  | OS 附带的 IddCx 版本 | 可运行的驱动程序的 IddCx 版本 |
| ----------  | ----------------------------- | ----------------------------- |
| 1607 (RS1)  | 1.0  | 1.0 |
| 1703 (RS2)  | 1.0  | 1.0 |
| 1709 (RS3)  | 1.2  | 1.0 和1。2 |
| 1803 (RS4)   | 1.3  | 1.0-1.3 和 1.4 ( * )  |
| 1809 (RS5)   | 1.3  | 1.0-1.3 和 1.4 ( * )  |
| 1903 (19H1)  | 1.4  | 1.0-1.3 和 1.4 ( * )  |
| 1909 (19H2)  | 1.4  | 1.0-1.3 和 1.4 ( * )  |
| 2004 (20H1)  | 1.4  | 1.0-1.3 和 1.4 ( * )  |
| 空值         | 1.6  | 1.0-1.3 和 1.4 ( * )  |

**\*** IddCx 1.4 和更高版本的 IDD 需要使用动态宏（如 IDD_IS_FUNCTION_AVAILABLE ( # A1）来决定运行时可以调用的操作系统功能。 这些动态宏是在 *iddcx*中定义的。

若要支持所有可能的 Windows 版本：

* 编写适用于 Windows 10 的 IddCx 1.0 驱动程序，版本1607到1709。
* 为 Windows 10、版本1803及更高版本写入单一 IddCx 1.4 或更高版本的驱动程序。