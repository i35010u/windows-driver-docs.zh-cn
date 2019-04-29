---
title: 可选命令
description: 可选命令
ms.assetid: b9c411b1-0061-468a-b900-47c6062aa3b0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d879fbc47d03a6beac72c49f204c4cf702a02481
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379655"
---
# <a name="optional-commands"></a>可选命令


## <span id="ddk_optional_commands_si"></span><span id="DDK_OPTIONAL_COMMANDS_SI"></span>


以下命令可以由 microdriver，但它不需要执行此操作。

<span id="CMD_GETSUPPORTEDFILEFORMATS"></span><span id="cmd_getsupportedfileformats"></span>CMD\_GETSUPPORTEDFILEFORMATS  
由 WIA 平板驱动程序，以获得其他文件格式的调用。 传递的两个成员[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构应填写： **lVal**应设置为其他文件格式; 数**pGuid**应指向图像格式的 Guid 的数组。 为此数组分配的内存归 microdriver 和仅应释放它。

中列出的映像格式*wiadef.h*或可被定义为自定义格式。 请注意，因为的 BMP （文件） 和 MEMORYBMP （内存） 的格式为所需的格式，WIA 平板驱动程序会自动添加它们。 Microdriver 应将它们添加到其扩展列表。

此命令是可选的除非设备可支持额外的文件格式。

<span id="CMD_GETSUPPORTEDMEMORYFORMATS"></span><span id="cmd_getsupportedmemoryformats"></span>CMD\_GETSUPPORTEDMEMORYFORMATS  
由 WIA 平板驱动程序，以获得更多的内存格式的调用。 传递的两个成员[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构应填写： **lVal**应设置为更多的内存格式; 数据格式的数**pGuid**应指向图像格式的 Guid 的数组。 为此数组分配的内存归 microdriver 和仅应释放它。

中列出的映像格式*wiadef.h*或可被定义为自定义格式。 请注意，因为的 BMP （文件） 和 MEMORYBMP （内存） 的格式为所需的格式，WIA 平板驱动程序会自动添加它们。 Microdriver 应将它们添加到其扩展列表。

此命令是可选的除非设备可支持额外的内存格式。

<span id="CMD_SETFORMAT"></span><span id="cmd_setformat"></span>CMD\_SETFORMAT  
在类驱动程序将发送此命令将当前格式设置应用程序的要求。 **PGuid**的成员[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构包含的图像格式的 GUID。 Microdriver 应将此映像格式 ID 保存在其专用的上下文中，以便跟踪的当前设置的图像格式。

Microdrivers 都需要支持此命令仅当报告扩展的格式。 由于类驱动程序具有无法验证扩展格式中的数据，它负责 microdriver 生成正确的数据。 在扩展格式中的数据传输时, 应传输所有数据，包括映像标头。 例如，如果您的驱动程序报告它支持的 JPEG 格式，则所有 JPEG 必须进行传输，而不仅仅是图像位。

在类驱动程序拥有通过指向的内存**pGuid** VAL 结构，因此 microdriver 必须释放它的成员。

请注意，此命令不影响 microdriver 响应对的调用的方法及其[**扫描**](https://msdn.microsoft.com/library/windows/hardware/ff547322)函数。 像往常一样，microdriver 必须检查的值*lPhase*， *pScanInfo*，并*lLength*指向此函数和放置数据的缓冲区中的参数*pBuffer*并*pReceived*作为适当的参数。

支持 WiaImgFmt 中只有文件的驱动程序\_BMP 和 WiaImgFmt\_MEMORYBMP 格式 （microdrivers 的默认格式） 可以接收 CMD\_SETFORMAT 命令。 这些驱动程序可以忽略此命令中，因为类驱动程序将处理所有数据传输使用的默认格式。

<span id="CMD_SETSCANMODE"></span><span id="cmd_setscanmode"></span>CMD\_SETSCANMODE  
由 WIA 平板驱动程序设置扫描模式-preview 或最终-microdriver 的设备的调用。 **LVal**的成员[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构将包含这两个定义中的以下值之一*wiamicro.h*:

扫描模式\_PREVIEWSCAN − 预览扫描模式

扫描模式\_FINALSCAN − 最终扫描模式

<span id="CMD_SETSTIDEVICEHKEY"></span><span id="cmd_setstidevicehkey"></span>CMD\_SETSTIDEVICEHKEY  
由 WIA 平板驱动程序，以允许 microdriver 读取注册表项中的已安装的注册表部分调用。 此命令提供了 STI 设备的已安装的注册表 HKEY 到 microdriver，以便它可以访问其设备的专用注册表值。 **PHandle**的成员[ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)结构将包含指向 STI 的期间指定给 WIA 平板驱动程序的 HKEY [ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)方法。 这是已安装的设备部分的顶级 HKEY。 **DeviceData**可以直接使用此 HKEY 打开密钥。 请参阅[WIA 设备 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542770)有关详细信息。

注意：此键是打开和关闭*仅*WIA 平板驱动程序。 它也是有效仅在此命令和 CMD\_初始化 (请参阅[所需命令](required-commands.md))。 这些命令返回后，该密钥不再有效。 HKEY 值*不得*缓存。

 

 





