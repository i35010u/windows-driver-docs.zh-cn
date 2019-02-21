---
Description: Installing the WpdMultiTransportDriver Sample
title: 安装 WpdMultiTransportDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba6081ea0ed411e29a35ed005ecda39c5a0d2f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521807"
---
# <a name="installing-the-wpdmultitransportdriver-sample"></a>安装 WpdMultiTransportDriver 示例


与其他 WPD 示例类似，此示例驱动程序安装为根枚举设备。 它将显示在**便携设备**或**WPD**中的节点**设备管理器**，与设备 ID 的根\\WPD\\NNNN。

### <a name="span-iddriverinstallationstepsspanspan-iddriverinstallationstepsspanspan-iddriverinstallationstepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>驱动程序安装步骤

完成安装的示例驱动程序的以下步骤：

1.  启动从所需的生成环境**启动**菜单。
2.  生成示例 ("build-cZ")。
3.  复制*WUDFUpdate\_0xxxx.dll*到包含驱动程序 DLL 的目录。 可以在中找到此&lt;WDK 安装路径&gt;\\redist\\wdf\\&lt;体系结构&gt;目录。
4.  安装驱动程序 ("devcon 安装 wpdmultitransportdriver.inf WUDF\\MultiTransport")。

请注意，驱动程序的 INF 文件中的 devcon 命令的最后一个参数对应于以下条目。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\MultiTransport
```

### <a name="span-iddriverremovalstepsspanspan-iddriverremovalstepsspanspan-iddriverremovalstepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>驱动程序删除步骤

完成以下步骤，若要删除的示例驱动程序：

1.  打开**设备管理器**。
2.  下**便携设备**节点中，单击你想要卸载的驱动程序。
3.  单击“卸载” 。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WpdMultiTransportDriverSample](the-wpdmultitransportdriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





