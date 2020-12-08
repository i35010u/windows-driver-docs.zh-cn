---
title: Windows 按钮数组的特定于设备的方法 (_DSM)
description: 为了支持 Windows 按钮用户界面 (UI) 的演变，Windows 使用本文中所述的函数为 Windows 按钮阵列设备定义 Device-Specific 方法 (_DSM) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9532eaca0603cbe9ead7562f5f0605d499f4d5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809727"
---
# <a name="windows-button-array-device-specific-method-_dsm"></a>Windows button array Device-Specific 方法 (\_ DSM) 


为了支持 Windows 按钮用户界面 (UI) 的演变，Windows \_ 使用本文中所述的函数为 windows 按钮阵列设备 (DSM) 定义 Device-Specific 方法。

## <a name="function-1-power-button-properties"></a>函数1：电源按钮属性


\_Power button properties 函数的 DSM 控制方法参数如下所示：

### <a name="arguments"></a>自变量

-   **Arg0：** UUID = dfbcf3c5-e7a5-44e6-9c1f-29c76f6e059c
-   **Arg1：** 修订版 ID = 0
-   **Arg2：** 函数 index = 1
-   **Arg3：** 空包 (未使用) 

### <a name="return"></a>返回

具有以下位字段定义 (DWORD) 的整数：

-   Bits 31 到33：保留 (必须为 0) 。
-   Bit 2：如果将 "电源" 按钮配置为检测按下和释放事件，并向操作系统报告这些事件，则应将此位设置为1。 否则，此位应为0。
-   位1：如果电源按钮连接到中断控制器 (GPIO 或其他) 支持级别检测，则应将此位设置为1。 否则，此位应为0。
-   位0：如果平台支持 ACPI 电源按钮替代时间为10秒或更长时间，则应将此位设置为1。 否则，此位应为0。

**注意**  每个 DSM 的函数索引 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关详细信息，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)中的 9.14.1 "DSM (设备特定方法) " 部分。

 

 

 




