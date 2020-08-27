---
description: 安装 WpdMultiTransportDriver 示例
title: 安装 WpdMultiTransportDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2373f06e50e908b1cb76b6962906bb325234c8e5
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969440"
---
# <a name="installing-the-wpdmultitransportdriver-sample"></a>安装 WpdMultiTransportDriver 示例


类似于其他 WPD 示例，此示例驱动程序作为根枚举设备安装。 它显示在**设备管理器**中的**便携设备**或**WPD**节点下，其设备 ID 为 ROOT \\ WPD \\ NNNN。

### <a name="span-iddriver_installation_stepsspanspan-iddriver_installation_stepsspanspan-iddriver_installation_stepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>驱动程序安装步骤

完成以下步骤来安装示例驱动程序：

1.  从 " **开始** " 菜单启动所需的生成环境。
2.  生成 ( "build – cZ" ) 的示例。
3.  将 *WUDFUpdate \_0xxxx.dll* 复制到包含驱动程序 DLL 的目录中。 可在 &lt; WDK 安装路径， &gt; \\ \\ wdf \\ &lt; 体系结构 &gt; 目录中找到此项。
4.  安装驱动程序 ( "devcon install wpdmultitransportdriver WUDF \\ MultiTransport" ) 。

请注意，devcon 命令的最后一个参数对应于驱动程序的 INF 文件中的以下条目。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\MultiTransport
```

### <a name="span-iddriver_removal_stepsspanspan-iddriver_removal_stepsspanspan-iddriver_removal_stepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>驱动程序删除步骤

完成以下步骤以删除示例驱动程序：

1.  打开 **设备管理器**。
2.  在 " **便携设备** " 节点下，单击要卸载的驱动程序。
3.  单击“卸载”  。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdMultiTransportDriverSample](the-wpdmultitransportdriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





