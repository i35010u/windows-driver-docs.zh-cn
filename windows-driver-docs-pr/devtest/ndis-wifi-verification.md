---
title: NDIS/WIFI 验证
description: NDIS/WIFI 验证选项确定 NDIS 或 WIFI 驱动程序是否正确与 Windows 操作系统内核交互。
ms.assetid: EB553449-9460-403D-8ED2-343048C4B38C
ms.date: 04/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6b6b0ed2566c9383d7e747584bc4dda9a7dc657d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381595"
---
# <a name="ndiswifi-verification"></a>NDIS/WIFI 验证

NDIS/WIFI 验证选项确定 NDIS 或 WIFI 驱动程序是否正确与 Windows 操作系统内核交互。

**注意**   此选项可从 Windows 8.1 开始使用。

NDIS/WIFI 验证选项应用规则，以验证您的驱动程序是否正确处理各种环境中的 Oid，并遵循 Microsoft 推荐的最佳做法。

如果此选项处于活动状态，并且驱动程序验证器检测到驱动程序违反了某个 NDIS 或 WIFI 规则，则驱动程序验证程序问题会检查 0xC4 (，参数1等于特定符合性规则的标识符) 。

验证规则列表包括以下各项：

[**NdisOidComplete**](./ndis-ndisoidcomplete.md)

[**NdisOidDoubleComplete**](./ndis-ndisoiddoublecomplete.md)

[**NdisOidDoubleRequest**](./ndis-ndisoiddoublerequest.md)

[**NdisTimedDataHang**](./ndis-ndistimeddatahang.md)

[**NdisTimedDataSend**](./ndis-ndistimeddatasend.md)

[**NdisTimedOidComplete**](./ndis-ndistimedoidcomplete.md)

[**WlanAssert**](./ndis-wlanassert.md)

[**WlanAssociation**](./ndis-wlanassociation.md)

[**WlanConnectionRoaming**](./ndis-wlanconnectionroaming.md)

[**WlanDisassociation**](./ndis-wlandisassociation.md)

[**WlanTimedAssociation**](./ndis-wlantimedassociation.md)

[**WlanTimedConnectionRoaming**](./ndis-wlantimedconnectionroaming.md)

[**WlanTimedConnectRequest**](./ndis-wlantimedconnectrequest.md)

[**WlanTimedScan**](./ndis-wlantimedscan.md)

[**WlanTimedLinkQuality**](./ndis-wlantimedlinkquality.md)

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 NDIS/WIFI 验证功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 你必须重新启动计算机以激活或停用 NDIS/WIFI 验证选项。

-   **在命令行中**

    在命令行中，NDIS/WIFI 验证由 **verifier/flags 0x200000** (位 21) 表示。 若要激活 NDIS/WIFI 验证，请使用0x200000 的标志值或将0x200000 添加到标志值。 例如：

    ```
    verifier /flags 0x200000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置") ** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **NDIS/WIFI 验证**。
    5.  重新启动计算机。

 

