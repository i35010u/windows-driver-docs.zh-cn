---
Description: 中心测试的目标是从设备中生成一组完整的可能的通信模式。 你可以测试通过添加上游的 SuperMUTT 包来断开连接的方案。
title: 测试与 MUTT 设备的 USB 集线器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a153cc9039ce5787d07348e8d56a5c7f1ac9b0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342164"
---
# <a name="usb-hub-testing-with-mutt-devices"></a>测试与 MUTT 设备的 USB 集线器


中心测试的目标是从设备中生成一组完整的可能的通信模式。 你可以测试通过添加上游的 SuperMUTT 包来断开连接的方案。

## <a name="hub-testing-prerequisites"></a>中心测试先决条件


在提升的命令提示符处运行 MUTT 测试命令之前，请确保满足以下要求：

-   测试系统必须运行 Windows 8 的最新版本。
-   设置和配置 MUTT 设备并安装固件。 有关详细信息，请参阅[如何进行准备，测试系统运行的测试工具的 MUTT](mutt-testing-options.md)。

## <a name="recommended-hub-tests"></a>推荐的中心测试


-   USB IF 电气测试。 所有我们的测试都是协议和已设定焦点的状态。 请参阅[USB-如果符合性计划](http://www.usb.org/developers/compliance/)的电气测试的详细信息。
-   MUTT 压力和传输测试包含在 MUTT 软件包 MUTT 设备连接的 USB 控制器建议的配置中。 **RunTest.bat**运行压力和传输的测试。 请参阅[如何运行压力和传输 MUTT 设备的性能测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)。
-   设备基本测试。 有关详细信息，请参阅[如何为 MUTT 设备运行 Visual Studio 中的说明测试](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)。
-   控制器 Windows 硬件认证工具包测试。 有关详细信息，请参阅[USB-如果证书验证测试 （控制器）](https://go.microsoft.com/fwlink/p/?linkid=316509)。
-   对于主机控制器，在部分中的 Windows 测试指南文档中找到的手动测试用例。

## <a name="recommended-topologies-for-hub-testing-with-mutt-devices"></a>建议使用 MUTT 设备进行测试的中心的拓扑


-   将 MUTT 设备附加到下游的每个可用端口。
-   将 Supermutt 附加到一半的可用端口。 将 MUTT 设备附加到剩余的端口。
-   附加待测试的中心的上游 SuperMutt 包和下游端口都具有同等数量的 SuperMUTT 和 MUTT 设备，如下图中所示：

    ![测试连接/断开连接](images/fig14-topology-connect-disconnect.png)

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



