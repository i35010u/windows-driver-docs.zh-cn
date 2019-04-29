---
Description: 安装 WpdServiceSampleDriver 示例
title: 安装 WpdServiceSampleDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da1b6877bb4a78941a117f5e089baf37c08cb203
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370490"
---
# <a name="installing-the-wpdservicesampledriver-sample"></a>安装 WpdServiceSampleDriver 示例


与其他 WPD 示例类似，此示例驱动程序将安装为根枚举设备。 它将显示在**便携设备**或**WPD**具有设备 ID 的根节点在设备管理器中，\\WPD\\NNNN。

### <a name="span-iddriverinstallationstepsspanspan-iddriverinstallationstepsspanspan-iddriverinstallationstepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>驱动程序安装步骤

完成安装的示例驱动程序的以下步骤：

1.  启动从所需的生成环境**启动**菜单。
2.  生成示例 ("build-cZ")。
3.  复制*WUDFUpdate\_0xxxx.dll*从&lt;WDK\_安装\_位置&gt;\\redist\\wdf\\ &lt;体系结构&gt;目录包含驱动程序 DLL 的目录。
4.  安装驱动程序 ("devcon 安装 wpdservicesampledriver.inf WUDF\\WpdService")

请注意 devcon 命令的最后一个参数对应于位于驱动程序的 INF 文件中的以下条目。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\WpdService
```

### <a name="span-iddriverremovalstepsspanspan-iddriverremovalstepsspanspan-iddriverremovalstepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>驱动程序删除步骤

完成以下步骤，若要删除的示例驱动程序：

1.  打开**Windows 设备管理器**。
2.  下**便携设备**节点中，单击你想要删除的驱动程序。
3.  单击“卸载” 。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[The WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





