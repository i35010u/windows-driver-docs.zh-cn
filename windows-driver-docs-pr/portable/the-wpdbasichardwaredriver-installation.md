---
Description: Installing the Sample Driver
title: 安装示例驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b941ddd5d1ee3bc51b8b9e5a3b4fa69184725b0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519772"
---
# <a name="installing-the-sample-driver"></a>安装示例驱动程序


与其他 Windows 便携式设备 (WPD) 示例类似，此示例驱动程序将安装为根枚举设备。 在便携式设备或 WPD 节点下中将出现**设备管理器**，并且具有设备 ID 的根\\WPD\\NNNN。

安装根枚举设备时，可以获取始终连接的设备。 因此，即使从 RS-232 端口传感器设备被拔出，设备节点 (devnode) 不会删除。 若要支持 devnode 到达 （或删除） 时 RS-232 连接插入 （或拔出），必须提供插即用 (PnP) 总线枚举器。 WDK Toaster 示例随附了示例总线枚举器。

安装 INF 文件中的示例驱动程序基于为 WpdHelloWorldDriver 的 INF 文件。 所做的更改的大多数都涉及使用 WpdBasicHardwareDriver WpdHelloWorldDriver 的字符串替换。 以下各节中总结了更显著的更改。

### <a name="span-idenablingfile-handletargetsspanspan-idenablingfile-handletargetsspanspan-idenablingfile-handletargetsspanenabling-file-handle-targets"></a><span id="Enabling_File-Handle_Targets"></span><span id="enabling_file-handle_targets"></span><span id="ENABLING_FILE-HANDLE_TARGETS"></span>启用文件句柄目标

下添加以下条目\[*基本\_Install.Wdf* \]来使文件句柄基于 UMDF I/O 目标。 这些 I/O 目标用于通过使用 RS 232 端口来与设备交换数据。 有关 I/O 目标的详细信息，请参阅[支持 I/O](the-wpdbasichardwaredriver-supporting-io.md)。

```cpp
UmdfDispatcher = FileHandle
```

### <a name="span-iddisablinglegacywiasupportspanspan-iddisablinglegacywiasupportspanspan-iddisablinglegacywiasupportspandisabling-legacy-wia-support"></a><span id="Disabling_Legacy_WIA_Support"></span><span id="disabling_legacy_wia_support"></span><span id="DISABLING_LEGACY_WIA_SUPPORT"></span>禁用旧版 WIA 支持

以下行注释掉，以禁用 Windows 图像采集 (WIA) 访问此驱动程序，因为示例驱动程序不支持图像内容的旧版应用程序：

```cpp
;HKR,,”EnableLegacySupport”,0x10001,1
```

### <a name="span-idinstallingthedriverspanspan-idinstallingthedriverspanspan-idinstallingthedriverspaninstalling-the-driver"></a><span id="Installing_the_Driver"></span><span id="installing_the_driver"></span><span id="INSTALLING_THE_DRIVER"></span>安装驱动程序

若要安装的示例驱动程序，请完成以下步骤：

1.  从**启动**菜单中，打开所需的生成环境。
2.  生成示例 ("build-cZ")。
3.  复制*WUDFUpdate\_0xxxx.dll*从&lt;WDK 安装位置&gt;\\redist\\wdf\\&lt;体系结构&gt;目录更改为包含驱动程序的 DLL 的目录。
4.  安装驱动程序 ("devcon 安装*Wpdbasichardwaredriver.inf* WUDF\\WpdBasicHardware")

**请注意**  devcon 命令的最后一个参数从驱动程序的 INF 文件对应于以下摘录。

 

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\WpdBasicHardware
```

### <a name="span-idremovingthedriverspanspan-idremovingthedriverspanspan-idremovingthedriverspanremoving-the-driver"></a><span id="Removing_the_Driver"></span><span id="removing_the_driver"></span><span id="REMOVING_THE_DRIVER"></span>删除驱动程序

若要删除的示例驱动程序，请完成以下步骤：

1.  打开 Windows 设备管理器。
2.  右键单击在驱动程序**便携设备**节点，然后单击**卸载**。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





