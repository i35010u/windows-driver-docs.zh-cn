---
title: 在 WBDI 驱动程序中支持安全通道
description: 在 WBDI 驱动程序中支持安全通道
keywords:
- 生物识别驱动程序 WDK，安全通道
- 安全通道 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf2f69cb11718cd6a452609580955133e226f97f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798613"
---
# <a name="supporting-secure-channels-in-wbdi-drivers"></a>在 WBDI 驱动程序中支持安全通道


若要在 WBDI 驱动程序中支持主机和设备之间的安全通道，必须将安全相关的功能封装到驱动程序中。 然后，该驱动程序将管理安全通道。 当驱动程序将示例数据传递到 Windows 生物识别服务 (WBS) 时，数据必须是未加密的。 WBS 中供应商提供的引擎插件可以根据需要设置 web 服务的安全通道。

安全注意事项应对 WBF 应用程序而言是透明的。

 

 





