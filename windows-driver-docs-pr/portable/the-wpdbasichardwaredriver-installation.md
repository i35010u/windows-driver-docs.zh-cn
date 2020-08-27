---
description: 安装示例驱动程序
title: 安装示例驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f4f5bde9854c5b2fdae53cd1b7c10bf3be631ad
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969338"
---
# <a name="installing-the-sample-driver"></a>安装示例驱动程序


类似于其他 Windows 便携式设备 (WPD) 示例，此示例驱动程序作为根枚举设备安装。 它显示在 **设备管理器**中的便携设备或 WPD 节点下，并且具有 WPD 的设备 ID \\ \\ 。

安装根枚举设备时，将获得一个始终连接的设备。 因此，即使传感器设备已从 RS-232 端口中拔出，也不会删除 (devnode) 的设备节点。 若要支持 (或删除) RS-232 连接接通电源 (或拔下) ，则必须提供即插即用 (PnP) 总线枚举器。 随 WDK Toaster 示例提供了示例总线枚举器。

示例驱动程序的安装 INF 文件基于 WpdHelloWorldDriver 的 INF 文件。 大多数更改都涉及到 WpdHelloWorldDriver 的字符串替换 WpdBasicHardwareDriver。 在以下各节中汇总了更重要的更改。

### <a name="span-idenabling_file-handle_targetsspanspan-idenabling_file-handle_targetsspanspan-idenabling_file-handle_targetsspanenabling-file-handle-targets"></a><span id="Enabling_File-Handle_Targets"></span><span id="enabling_file-handle_targets"></span><span id="ENABLING_FILE-HANDLE_TARGETS"></span>启用文件句柄目标

将在 "基本" Install 下添加以下条目 \[ * \_ * \] ，以启用基于文件句柄的 UMDF i/o 目标。 这些 i/o 目标用于通过 RS 232 端口与设备交换数据。 有关 i/o 目标的详细信息，请参阅 [支持 i/o](the-wpdbasichardwaredriver-supporting-io.md)。

```cpp
UmdfDispatcher = FileHandle
```

### <a name="span-iddisabling_legacy_wia_supportspanspan-iddisabling_legacy_wia_supportspanspan-iddisabling_legacy_wia_supportspandisabling-legacy-wia-support"></a><span id="Disabling_Legacy_WIA_Support"></span><span id="disabling_legacy_wia_support"></span><span id="DISABLING_LEGACY_WIA_SUPPORT"></span>禁用旧版 WIA 支持

以下行被注释掉，以禁用 Windows 图像采集 (WIA) 旧版应用程序访问此驱动程序，因为示例驱动程序不支持图像内容：

```cpp
;HKR,,”EnableLegacySupport”,0x10001,1
```

### <a name="span-idinstalling_the_driverspanspan-idinstalling_the_driverspanspan-idinstalling_the_driverspaninstalling-the-driver"></a><span id="Installing_the_Driver"></span><span id="installing_the_driver"></span><span id="INSTALLING_THE_DRIVER"></span>安装驱动程序

若要安装示例驱动程序，请完成以下步骤：

1.  从 " **开始** " 菜单中，打开所需的生成环境。
2.  生成 ( "build – cZ" ) 的示例。
3.  将*WUDFUpdate \_0xxxx.dll*从 &lt; WDK 安装位置 "已再发行的 &gt; \\ \\ wdf \\ &lt; 体系结构" &gt; 目录复制到包含驱动程序的 DLL 的目录中。
4.  安装驱动程序 ( "devcon install *Wpdbasichardwaredriver* WUDF \\ WpdBasicHardware" ) 

**注意**   Devcon 命令的最后一个参数对应于驱动程序的 INF 文件中的以下摘录。

 

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\WpdBasicHardware
```

### <a name="span-idremoving_the_driverspanspan-idremoving_the_driverspanspan-idremoving_the_driverspanremoving-the-driver"></a><span id="Removing_the_Driver"></span><span id="removing_the_driver"></span><span id="REMOVING_THE_DRIVER"></span>删除驱动程序

若要删除示例驱动程序，请完成以下步骤：

1.  打开 Windows 设备管理器。
2.  右键单击 " **可移植设备** " 节点下的驱动程序，然后单击 " **卸载**"。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





