---
ms.assetid: A8888EF1-5A6F-4B08-8743-27EEECD4FF72
title: 预配计算机时会出现什么情况 (WDK 8.0)
description: 这里我们将介绍在使用 Windows 驱动程序工具包 (WDK) 8.0 版预配目标计算机时发生的情况。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4effdc9c3609072ea8f82aab32987889bd2b5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518375"
---
# <a name="what-happens-when-you-provision-a-computer-wdk-80"></a>预配计算机时会出现什么情况 (WDK 8.0)

使用 Microsoft Visual Studio 配置和设置驱动程序部署和驱动程序测试称为“预配目标计算机”或“预配测试计算机”。 有关使用 Windows 驱动程序工具包 (WDK) 8 预配的信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh698272)。 这里我们将介绍在使用 Windows 驱动程序工具包 (WDK) 8.0 版预配目标计算机时发生的情况。

**注意**  WDK 8 不是 WDK 的最新版本。 我们建议你获取当前版本的 WDK，并根据[此处的预配说明](https://msdn.microsoft.com/Library/Windows/Hardware/Hh698272)预配目标计算机。

 

## <a name="span-idwhenyouprovisionacomputerwdk80spanspan-idwhenyouprovisionacomputerwdk80spanwhen-you-provision-a-computer-wdk-80"></a><span id="when_you_provision_a_computer_wdk_8_0"></span><span id="WHEN_YOU_PROVISION_A_COMPUTER_WDK_8_0"></span>预配计算机时 (WDK 8.0)


预配计算机将执行以下任务：

-   将安装文件复制到 %SystemDrive%\\DriverTest
-   创建名为 WDKRemoteUser 的用户，并切换到该用户
-   安装 .NET 4.0（如果未安装）
-   安装 Microsoft Visual C++ Redistributable
-   安装[测试创作和执行框架 (TAEF)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439725)（WDK 客户端）
-   安装调试程序
-   安装 [Windows 设备测试框架](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547) (WDTF)
-   关闭 AutoReboot
-   启用内核内存故障转储
-   禁用屏幕保护程序
-   禁用工作站锁定策略
-   禁用 ForceGuest
-   将电源策略设置为高功率配置，这将阻止系统在空闲状态时进入“待机”或“休眠”模式
-   启用“RTC 唤醒”计时器
-   启用并配置内核调试
-   启用驱动程序测试签名
-   如有必要，重新启动目标计算机
-   创建系统还原点

## <a name="span-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanremoving-provisioning-from-the-target-computer"></a><span id="Removing_provisioning_from_the_target_computer"></span><span id="removing_provisioning_from_the_target_computer"></span><span id="REMOVING_PROVISIONING_FROM_THE_TARGET_COMPUTER"></span>从目标计算机中删除预配


预配目标计算机后，将无法完全删除预配。 但是，可以使用主计算机上的 Visual Studio 从目标计算机上删除大部分预配。 以下是操作步骤。

1.  在主计算机上，在 Visual Studio 的“驱动程序”菜单中，选择“测试”&gt;“配置计算机”。
2.  选择目标计算机的名称，然后单击“删除计算机”。
3.  选择“删除预配并删除计算机”。 单击“下一步” 。
4.  完成删除过程后，单击“完成”。

## <a name="span-idwhenyouremoveprovisioningwdk80spanspan-idwhenyouremoveprovisioningwdk80spanwhen-you-remove-provisioning-wdk-80"></a><span id="when_you_remove_provisioning__wdk_8.0_"></span><span id="WHEN_YOU_REMOVE_PROVISIONING__WDK_8.0_"></span>删除预配时 (WDK 8.0)


从目标计算机中删除预配时，会删除以下项目：

-   Visual C++ Redistributable
-   测试自动化框架
-   调试程序
-   Windows 驱动程序测试框架
-   %SystemDrive%\\DriverTest 文件夹和内容
-   WDKRemoteUser 帐户

删除预配不会更改以下项目：

-   AutoReboot 设置
-   内核内存故障转储设置
-   屏幕保护程序设置
-   工作站锁定策略
-   ForceGuest 设置
-   电源策略
-   “RTC 唤醒”计时器设置
-   内核调试设置
-   测试签名设置

 

 





